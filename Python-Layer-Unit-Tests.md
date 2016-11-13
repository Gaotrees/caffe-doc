#How-To

This article covers how to unit test a simple Python Layer. We will test the forward pass of the `AccuracyLayer` Python layer helpfully shared by [lukeyeager](https://github.com/lukeyeager).  

In this `how-to`, locations for the python files are suggested but note that these are are entirely optional provided you modify the necessary environment variables.

Begin by creating a file at `python/caffe/py_accuracy_layer.py` and add the following code (this layer was written by @lukeyeager, you can find his orignal [here](https://gist.github.com/lukeyeager/5ae183044d96ef1540f2)):

```
import caffe
import json
	
class AccuracyLayer(caffe.Layer):
    """
    Rewrite Accuracy layer as a Python layer
    Accepts JSON-encoded parameters through param_str
    Use like this:
    layer {
        name: "accuracy"
        type: "Python"
        bottom: "pred"
        bottom: "label"
        top: "accuracy"
        include {
            phase: TEST
        }
        python_param {
            module: "accuracy_layer"
            layer: "AccuracyLayer"
            param_str: "{\"top_k\": 2}"
        }
    }
    """
    
    def setup(self, bottom, top):
        assert len(bottom) == 2,    'requires two layer.bottoms'
        assert len(top) == 1,       'requires a single layer.top'
    
        if hasattr(self, 'param_str') and self.param_str:
            params = json.loads(self.param_str)
        else:
            params = {}
	
        self.top_k = params.get('top_k', 1)
    
    def reshape(self, bottom, top):
        top[0].reshape(1)
    
    def forward(self, bottom, top):
        # Renaming for clarity
        predictions = bottom[0].data
        ground_truth = bottom[1].data
    
        num_correct = 0.0
    
        # NumPy magic - get top K predictions for each datum
        top_predictions = (-predictions).argsort()[:, :self.top_k]
        for batch_index, predictions in enumerate(top_predictions):
            if ground_truth[batch_index] in predictions:
                num_correct += 1
    
        # Accuracy is averaged over the batch
        top[0].data[0] = num_correct / len(ground_truth)
    
    def backward(self, top, propagate_down, bottom):
        pass
```

This layer takes in predictions and labels and uses them to compute an accuracy score.  With the python layer in place, we can set about creating the layer tests.  Begin by creating a file at `python/caffe/test_py_accuracy_layer.py`.	

## Imports

The following code imports the libraries needed by our test code:

```
import os
import unittest
import tempfile
import numpy as np
import caffe
from caffe import layers as L
```

## Boilerplate

Python is a second class citizen when it comes to the ability to unit test it with Caffe. In C++ we are able to instantiate a Layer, set up the bottom blobs, and forward our single layer. In Python we have to work around with a simple NetSpec. (I could be wrong about this and if I determine a way to instantiate a Python Layer directly and unit test it comfortably I will update this.)

For our testing we will need to add two boilerplate functions.  The first takes in a prototxt string (describing a net), and returns a `Net` object:

```
def load_net(net_proto):
    f = tempfile.NamedTemporaryFile(mode='w+', delete=False)
    f.write(str(net_proto))
    f.close()
    return caffe.Net(f.name, caffe.TEST)
```

The second function will make a prototxt string (describing a network). Here, we use a dummy layer that outputs two `tops` and our Python Layer that accepts the two `tops` and outputs one `bottom`.

```
def example_network(batch_size):
    n = caffe.NetSpec()

    # we use the dummy data layer to control the 
    # shape of the inputs to the layer we are testing
    ip_dims = [batch_size, 3]
    label_dims = [batch_size]
    n.ip, n.label = L.DummyData(shape=[dict(dim=ip_dims),dict(dim=label_dims)],
                                        transform_param=dict(scale=1.0/255.0),
                                        ntop=2)

    # now we add the layer to be testsed
    n.accuracy = L.Python(n.ip, n.label,
                          python_param=dict(
                              module='caffe.py_accuracy_layer',  #YOUR .py FILE NAME HERE
                              layer='AccuracyLayer',             #YOUR CLASSNAME HERE
                              param_str='{\"top_k\": 1}'),       #JSON WITH YOUR PARAMS
                          ntop=1)
    return n.to_proto()
```



## Unit Test

With an example network using the layer in place, we can add our unit tests:

```
class BasicAccuracyTest(unittest.TestCase):
    def test_layer_creation(self):
        net_proto = example_network(batch_size=1)
        net = load_net(net_proto)
        self.assertIsNotNone(net)

    def test_accuracy_computation(self):
        INNER_PRODUCT_A = [1.0, 0.0, 0.0]
        INNER_PRODUCT_B = [1.0, 0.0, 0.0]
        ip_data = np.array([INNER_PRODUCT_A, INNER_PRODUCT_B])

        LABEL_A = 0
        LABEL_B = 1
        labels = np.array([LABEL_A, LABEL_B])

        net_proto = example_network(batch_size=2)
        net = load_net(net_proto)
        net.blobs['ip'].data[...] = ip_data
        net.blobs['label'].data[...] = labels
        net.forward()

        accuracy_data = net.blobs['accuracy'].data[0]

        self.assertEqual(accuracy_data, 0.5)  #We should get LABEL_A correct, but LABEL_B incorrect
```

Finally, we can check the tests pass by running `make pytest` in the caffe root directory.  If all has gone well, you well see a message that lists the timing statistics of the tests that have been run.