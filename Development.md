## Developing new layers

- Add a class declaration for your layer to the appropriate one of `common_layers.hpp`, `data_layers.hpp`, `loss_layers.hpp`, `neuron_layers.hpp`, or `vision_layers.hpp`. Include an inline implementation of `type` and the `*Blobs()` methods to specify blob number requirements. Omit the `*_gpu` declarations if you'll only be implementing CPU code.
- Implement your layer in `layers/your_layer.cpp`.
  * (optional) `LayerSetUp` for one-time initialization: reading parameters, fixed-size allocations, etc.
  * `Reshape` for computing the sizes of top blobs, allocating buffers, and any other work that depends on the shapes of bottom blobs
  * `Forward_cpu` for the function your layer computes
  * `Backward_cpu` for its gradient (Optional -- a layer can be forward-only)
- (Optional) Implement the GPU versions `Forward_gpu` and `Backward_gpu` in `layers/your_layer.cu`.
- Add your layer to `proto/caffe.proto`, updating the next available ID. Also declare parameters, if needed, in this file.
- Register your layer in your cpp file with the macro provided in `layer_factory.hpp`. Assuming that you have a new layer `MyAwesomeLayer` and the layer type in the proto is `AWESOME`, you can register it with the following command:
````
REGISTER_LAYER_CLASS(AWESOME, MyAwesomeLayer);
````
- Optionally, you can also register a Creator if your layer has multiple engines. For an example on how to define a creator function and register it, see `GetConvolutionLayer` in `caffe/layer_factory.cpp`.
- Write tests in `test/test_your_layer.cpp`. Use `test/test_gradient_check_util.hpp` to check that your Forward and Backward implementations are in numerical agreement.

## Forward-Only Layers
If you want to write a layer that you will only ever include in a test net, you do not have to code the backward pass. For example, you might want a layer that measures performance metrics at test time that haven't already been implemented.
Doing this is very simple. You can write an inline implementation of Backward_cpu (/Backward_gpu) together with the definition of your layer in include/<layertype>_layers.hpp that looks like:
````
virtual void Backward_cpu(const vector<Blob<Dtype>*>& top, const vector<bool>& propagate_down, vector<Blob<Dtype>*>* bottom) {
  NOT_IMPLEMENTED;
}
````
For examples, look at the accuracy layer (loss_layers.hpp) and threshold layer (neuron_layers.hpp) definitions.