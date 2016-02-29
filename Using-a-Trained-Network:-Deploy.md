# Using a Trained Network

A network is defined by it's design (.prototxt), and it's weights (.caffemodel). As a network is being trained, the current state of that network's weights are stored in a .caffemodel. With both of these we can move from the train/test phase into the production phase.

# Modifying the Network for Deployment

In it's current state, the design of the network is not designed for deployment. Before we can release our network as a product, we often need to alter it in a few ways:
1. Remove the data layer that was used for training, as for in the case of classification we are no longer providing labels for our data.
1. Remove any layer that is dependent upon data labels.
1. Set the network up to accept data.
1. Have the network output the result.

## Example: MNist

### Training/Testing

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
    
    layer {
      name: "accuracy"
      type: "Accuracy"
      bottom: "ip2"
      bottom: "label"
      top: "accuracy"
      include {
        phase: TEST
      }
    }
    layer {
      name: "loss"
      type: "SoftmaxWithLoss"
      bottom: "ip2"
      bottom: "label"
      top: "loss"
    }


