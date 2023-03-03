
Often models are still deployed on CPU (irratic production load and a delay of a few seconds not impacting the value of the product), but packages rarely include the details of this inference speed, instead stating something like training iters/second on an 8 gpu machine.

Here's a benchmark of all of the models in Detectron2, run on CPU and GPU. 
