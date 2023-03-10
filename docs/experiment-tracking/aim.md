## Why move beyond tensorboard? 

* Working as a team (possible but awkward) 
* Retrospective notes tied to specific runs. 
* Just a very nice UI. 


## How to integrate Aim 

Huge thanks to the Aim team (Gor, Gev, Mahnerak) for helping me see why I was creating a run in the Aim UI for each GPU, and how I could resolve it by checking if the current process was the 'main' process.

* You need use a hook
```
from detectron2.engine import HookBase
from aim import Run
import torch
import os
import detectron2.utils.comm as comm
from datetime import datetime

AIM_URL = os.environ["AIM_URL"]

class AimHook(HookBase):
    """
    A custom hook class that logs artifacts, metrics, and parameters to MLflow.
    
    All taken from https://philenius.github.io/machine%20learning/2022/01/09/how-to-log-artifacts-metrics-and-parameters-of-your-detectron2-model-training-to-mlflow.html
    And adapted for Aim
    
    Looking at write_metrics in this file can help with further development.
    https://github.com/facebookresearch/detectron2/blob/80e2673da161f57afe37ef769836a61976108ef1/detectron2/engine/train_loop.py#LL346
    """

    def __init__(self, cfg):
        super().__init__()
        self.cfg = cfg.clone()

    def before_train(self):
        
        clean_datetime = str(datetime.now()).replace(' ','_').replace(':','-')
        
        # Have to check if it's the main process so that you dont 
        # get multiple tracked run for a single, multi-gpu process.s
        if comm.is_main_process():
            self.run = Run(
                repo=AIM_URL,
                experiment=clean_datetime,
            )
            self.run['hparams'] = self.cfg

    def after_step(self):
        # Only write metrics if it's the main process
        if comm.is_main_process():
            with torch.no_grad():
                latest_metrics = self.trainer.storage.latest()
                for k, v in latest_metrics.items():
                    self.run.track(name=k, value=v[0], step=self.trainer.storage.iter)

    def after_train(self):
        with torch.no_grad():
            with open(os.path.join(self.cfg.OUTPUT_DIR, "model-config.yaml"), "w") as f:
                f.write(self.cfg.dump())
```

You then need to register this hook with your trainer 

aim_hook = AimHook(cfg) # feeding through the cfg object in order to track hyperparameters
trainer.register_hooks([aim_hook])
