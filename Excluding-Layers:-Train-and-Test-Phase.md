#Excluding Layers

Caffe can be told to include or exclude a layer when running a network in a particular `phase`.

For examples, when training a model with caffe via `caffe train ...`, or `caffe test ...`, we are explicitly telling caffe to train in a particular phase, train and test respectively.

There are times when a network should behave slightly differently depending on whether is being trained or being tested, and thus by setting the appropriate include-phase we can achieve this behaviour without having to define many nearly identical network prototxts.

## Example: MNist

The first two layers of the MNist example is presented. Note that the input data and batch size differs depending on the current phase.

    name: "LeNet"
    layer {
      name: "mnist"
      type: "Data"
      top: "data"
      top: "label"
      include {
        phase: TRAIN
      }
      transform_param {
        scale: 0.00390625
      }
      data_param {
        source: "examples/mnist/mnist_train_lmdb"
        batch_size: 64
        backend: LMDB
      }
    }
    layer {
      name: "mnist"
      type: "Data"
      top: "data"
      top: "label"
      include {
        phase: TEST
      }
      transform_param {
        scale: 0.00390625
      }
      data_param {
        source: "examples/mnist/mnist_test_lmdb"
        batch_size: 100
        backend: LMDB
      }
    }
    ...