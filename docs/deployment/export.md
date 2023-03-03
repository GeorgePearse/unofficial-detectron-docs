The repo comes with an unassuming script called export_model.py, it uses the rest of the package just as an API, and can be used as a standalone script or copied into your own repo (so that you don't have to clone detectron2).

It is overly verbose, so I've rewritten the core parts below with typer instead of python's default parser. 
It also just runs from a config.yaml (can obviously change the path to the weights here), but for my workflows that would normally point to the original weights that I started training from. Not my best checkpoint.
So I added an additional argument to point to those trained weights.
