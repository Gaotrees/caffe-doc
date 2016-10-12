#NetSpec

This article covers how to make Prototxt nets without having to look at a single protobuf message.

## Diving In

The following is a quick example that creates a prototxt (string; it still needs to be saved).

```
import caffe
from caffe import layers as L
from caffe import params as P

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


```
layer {
  name: "loss"
  type: "DummyData"
  top: "loss"
  dummy_data_param {
    shape {
      dim: 1
    }
  }
}
layer {
  name: "accuracy"
  type: "Python"
  bottom: "loss"
  top: "accuracy"
  python_param {
    module: "python_loss_graph"
    layer: "PythonLossGraph"
  }
}
```