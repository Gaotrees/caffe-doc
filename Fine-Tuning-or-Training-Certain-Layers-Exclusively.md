# Fine-Tuning

Fine-Tuning is the process of training specific sections of a network to improve results.

## Making Layers Not Learn

To stop a layer from learning further, you can set it's `param` attributes in your prototxt.

For example:

    layer {
      name: "example"
      type: "example" 
      ...
      param {
        lr_mult: 0    #learning rate of weights
        decay_mult: 1
      }
      param {
        lr_mult: 0    #learning rate of bias
        decay_mult: 0
      }
    }
    