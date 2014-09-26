Developing new layers
---------------------

1. Add a class declaration for your layer to the appropriate one of `common_layers.hpp`, `data_layers.hpp`, `loss_layers.hpp`, `neuron_layers.hpp`, or `vision_layers.hpp`. Include an inline implementation of `type` and the `*Blobs()` methods to specify blob number requirements. Omit the `*_gpu` declarations if you'll only be implementing CPU code.
2. Implement your layer in `layers/your_layer.cpp`.
  * (optional) `LayerSetUp` for one-time initialization: reading parameters, fixed-size allocations, etc.
  * `Reshape` for computing the sizes of top blobs, allocating buffers, and any other work that depends on the shapes of bottom blobs
  * `Forward_cpu` for the function your layer computes
  * `Backward_cpu` for its gradient
3. (Optional) Implement the GPU versions `Forward_gpu` and `Backward_gpu` in `layers/your_layer.cu`.
4. Add your layer to `proto/caffe.proto`, updating the next available ID. Also declare parameters, if needed, in this file.
5. Make your layer createable by adding it to `layer_factory.cpp`.
6. Write tests in `test/test_your_layer.cpp`. Use `test/test_gradient_check_util.hpp` to check that your Forward and Backward implementations are in numerical agreement.