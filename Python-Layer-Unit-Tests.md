#How-To

This article covers how to unit test a Python Layer. It does not cover how to install, or manage your Python Layer. We will be assuming that we have a class named `PythonAccuracy` in a file named `python_accuracy`.


## Boilerplate

Python is a second class citizen when it comes to ones ability to unit test it with Caffe. In C++ we are able to instantiate a Layer, set up the bottom blobs, and forward our single layer. In Python we have to work around with with a simple NetSpec. (I could be wrong about this and if I determine a way to instantiate a Python Layer directly and unit test it comfortably I will update this.)

For our testing we will need two boilerplate methods:

```
def load_net(net_proto):
    f = tempfile.NamedTemporaryFile(mode='w+', delete=False)
    f.write(str(net_proto))
    f.close()
    return caffe.Net(f.name, caffe.TEST)
```

This will take in a prototxt string (describing a net), and return a `net object`.

```
def example_network(batch_size):
    n = caffe.NetSpec()

    n.ip, n.label = L.DummyData(shape=[dict(dim=[batch_size, 3]),
                                               dict(dim=[batch_size, 1, 4, 4]),
                                               dict(dim=[batch_size])],
                                        transform_param=dict(scale=1.0/255.0),
                                        ntop=2)
    n.accuracy = L.Python(n.label, n.data,
                          python_param=dict(
                                          module='python_accuracy',    #YOUR .py FILE NAME HERE
                                          layer='PythonAccuracy',      #YOUR CLASSNAME HERE
                                          param_str='{ "param_name": param_value }'), #JSON WITH YOUR PARAMS
                          ntop=1,)

    return n.to_proto()
```

This will make a prototxt string (describing a network). Here, we make a dummy layer that outputs two `tops` and our Python Layer that accepts the two `tops` and outputs one `bottom`.

## Unit Test

Let's write our first unit test:

```
def test_layer_creation(self):
        net_proto = example_network(batch_size=1)
        net = load_net(net_proto)
        
        self.assertIsNotNone(net)

def test_incorrect_predictions_are_stored_in_folders(self):
        INNER_PRODUCT_A = [1.0, 0.0, 0.0]
        INNER_PRODUCT_A = [1.0, 0.0, 0.0]

        LABEL_A = 0
        LABEL_B = 1

        net_proto = example_network(batch_size=2)
        net = load_net(net_proto)

        net.blobs['ip'].data[...] = np.array([INNER_PRODUCT_A,
                                              INNER_PRODUCT_B])
        net.blobs['label'].data[...] = np.array([LABEL_A,LABEL_B])

        net.forward()

        accuracy_data = net.blobs['accuracy'].data[0]
        
        self.assertEqual(accuracy_data,0.5)  #We should get LABEL_A correct, but LABEL_B incorrect
```