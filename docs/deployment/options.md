# Deployment

## Options 

* Torchscript 
- Gotchas 
- Make sure to import torchscript before reloading the saved model 
- Show what would be hit, show successful reload. 

* ONNX 
- Because it's a 'universal' framework, it offers thje most functionality wrt further optimizations (e.g. operator fusing or conversion to fp16 or int8) 

## Preprocessing 
Within detectron2 preprocessing is managed by a predictor object, but if you're using torchscript or ONNX, you're trying to remove your 
dependence on detectron2. In order to achieve this aim I simply extracted the preprocessing code from the predictor object.

```

```
