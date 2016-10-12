#NetSpec

This article covers how to make Prototxt nets without having to look at a single protobuf message.

## Diving In

The following is a quick example that creates a prototxt (string; it still needs to be saved).

We first create a DummyData layer, which outputs n.loss and n.label ("loss" and "label" in the proto).

We then pass the outputs to the input of our Python layer, which itself outputs  n.accuracy ("accuracy" in the proto).

```
import caffe
from caffe import layers as L
from caffe import params as P

def example_network(batch_size):
    n = caffe.NetSpec()

    n.loss, n.label = L.DummyData(shape=[dict(dim=[1]),
                                         dict(dim=[1]),
                                  transform_param=dict(scale=1.0/255.0),
                                  ntop=2)

    n.accuracy = L.Python(n.loss, n.label,
                          python_param=dict(
                                          module='python_accuracy',
                                          layer='PythonAccuracy',
                                          param_str='{ "param_name": param_value }'),
                          ntop=1,)

    return n.to_proto()
```

Executing the above code will produce the following:

```
layer {
  name: "loss"
  type: "DummyData"
  top: "loss"
  top: "label"
  dummy_data_param {
    shape {
      dim: 1
    }
    shape {
      dim: 1
    }
  }
}
layer {
  name: "accuracy"
  type: "Python"
  bottom: "loss"
  bottom: "label"
  top: "accuracy"
  python_param {
    module: "python_loss_graph"
    layer: "PythonLossGraph"
  }
}
```