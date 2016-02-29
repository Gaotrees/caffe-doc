# Using a Trained Network

A network is defined by it's design (.prototxt), and it's weights (.caffemodel). As a network is being trained, the current state of that network's weights are stored in a .caffemodel. With both of these we can move from the train/test phase into the production phase.

# Modifying the Network for Deployment

In it's current state, the design of the network is not designed for deployment. Before we can release our network as a product, we often need to alter it in a few ways:
1. Remove the data layer that was used for training, as for in the case of classification we are no longer providing labels for our data.
1. Remove any layer that is dependent upon data labels.
1. Set the network up to accept data.
1. Have the network output the result.

## Example: MNist

Caffe comes with an examples folder. In our example we will be looking at the mnist network, specifically lenet_train_test.prototxt. The mnist network was highly successfully at classifying hand written digits.

### Training/Testing

The mnist network has two data layers, one designated for training and the other for testing, each of which specifies the location of an lmdb file where the images are stored. The output of the network is a Softmax with a Loss, that is to say it computer a probabilistic likelihood per class, and uses this to determine the error that the network has made. An Accuracy layer, on the other hand, is available at Test time to report the score of the network on the current batch.

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

### Deploying this Network

Following the previously stated steps, we can take this network to production.

#### Remove the Data Layer(s) That Were Used For Training.

These two layers are no longer valid, as we will not be providing labelled data:
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
    ....


becomes

    ....
