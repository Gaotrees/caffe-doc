# Using a Trained Network

A network is defined by its design (.prototxt), and its weights (.caffemodel). As a network is being trained, the current state of that network's weights are stored in a .caffemodel. With both of these we can move from the train/test phase into the production phase.

# Modifying the Network for Deployment

In its current state, the design of the network is not designed for deployment. Before we can release our network as a product, we often need to alter it in a few ways:

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

#### Remove any layer that is dependent upon data labels.

The Accuracy Layer and the SoftmaxWithLoss Layer are still expecting labels, but there are none to provide, thus there layers are no longer needed as well:

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

becomes

    ....

#### Set the Network Up To Accept Data.

The MNist data is of size 32x32 and in RGB. For simplicity we will keep the batch size at 1. This new data entry point in our network looks like this:

    input: "data"
    input_shape {
      dim: 1 # batchsize
      dim: 3 # number of colour channels - rgb
      dim: 32 # width
      dim: 32 # height
    }
    ...

This would be the first lines in the prototxt, following the network's name.

#### Have the network output the result.

Our network prior to this was computing a Softmax with Loss, and by all means we still want the Softmax. We can now add a new layer to the end of our network to produce a Softmax output:

    layer {
      name: "loss"
      type: "Softmax"
      bottom: "ip2"
      top: "loss"
    }

### Using the New Network

Now that our deployment network is complete, we can use it as originally intended. We want to provide it one 32x32 image with three color channels. To do this, we will use Matlab.

For example's sake we will be using the weights from net_4800.caffemodel (you'll have to train your own).

    model = 'deploy.prototxt';
    weights = 'net_4800.caffemodel';

    caffe.set_mode_gpu();
    caffe.set_device(0);
    
    net = caffe.Net(model, weights, 'test');

Now we have our network, we can give it a run, by providing it an image.

    image = imread('example_4.png');
    res = net.forward({image});
    prob = res{1};

If we take a look at prob, we should see a column of probabilities, where the 4th row has the highest value.

### If You Run Into Trouble

In the case of Matlab crashing, this is caused by a `Check(...)` in the caffe code. A `Check(...)` failure triggers an `abort()`, which Matlab takes very seriously. To diagnose what the problem is, start Matlab from a console window, so that you can see the caffe output. The issue will be immediately discoverable from the caffe network construction logs, and NOT from the Matlab logs in this case.