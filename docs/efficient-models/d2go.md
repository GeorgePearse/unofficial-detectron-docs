Detectron2 has a sister/brother package for mobile model deployment called d2go, it provides the functionality to train models with highly efficient backbones, and then export them to quantized torchscript format.

Really it's a good place to train models for any compute constrained environment.

I've found the package has some bugs for the latest version of torch (just import paths) so I keep my own fork here. 
