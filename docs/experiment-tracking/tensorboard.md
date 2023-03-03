
By default logs are tracked by Tensorboard. 

Tensorboard is incredibly stable and reliable due to its age and heavy use, but it is limited. The most significant limitation is how difficult it is to retrospectively add notes or tags to a run. 

Say your hyperparams are actually missing an important detail about the experiment. What are your options? How do you then record that? 

I'd also recommend saving the output to a folder named by ouput/<date-time>

That way when you run it with: 
```
tensorboard --logdir output --host=0.0.0.0 --port=6006
```

You'll be able to compare all of your experiments in one place. 
