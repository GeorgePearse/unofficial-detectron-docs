## Motivation

I've grown accustomed to documentation writen by open-source companies. These are excellently maintained, and more educational than simply descriptive. 

You are a potential customer, so good documentation is part of the product, this is often not the case for powerful ML repos and APIs (pytorch-lightning not included).

Even parts of the API that are well documented simply state what something is, not when you'd want to use it nor why you care. Why you care is how people learn. 

Dagster taught me a lot about Data Engineering, and pytorch-lightning via its callback setup and flags guides you towards all of the things that a respectable experimentation template should include (short epochs to test functionality, checkpointing to cloud etc.). Detectron2 provides the tooling you need to achieve this setup but not the handrails to get there. This is in contrast with the fact that it's arguably the easiest way to actually train an accurate object detection model. No worrying about stitching together a backbone and a prediction head, just specify the config via YAML and detectron2 sorts it out for you.
