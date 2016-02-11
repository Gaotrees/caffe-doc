# Making Your First Layer

In this page we will learn how to make a simple layer, and how to write a test for it. This will demonstrate some of the concepts in this framework and will exemplify how to use some of the components.

## The Layer

This layer will take in data from the bottom Blob, transform into new data and send it to the top Blob.

### The Header Definition

The typical includes and setup:

    #ifndef CAFFE_SIN_LAYER_HPP_
    #define CAFFE_SIN_LAYER_HPP_
    
    #include <vector>
    
    #include "caffe/blob.hpp"
    #include "caffe/layer.hpp"
    #include "caffe/proto/caffe.pb.h"
    
    #include "caffe/layers/neuron_layer.hpp"

    namespace caffe {
    
    template <typename Dtype>
    class SinLayer : public NeuronLayer<Dtype> {
     public:
      explicit SinLayer(const LayerParameter& param)
          : NeuronLayer<Dtype>(param) {}

A method that must be overridden. This is necessary to link the protobuf code to your C++ code. Essentially you are creating an identifier that will act as a link this layer to the framework. The must be unique and should be named after your layer, not including the "Layer" part ie. `"sin_layer"` becomes `"Sin"`.  
    
      virtual inline const char* type() const { return "Sin"; }

These methods must be overridden as well. They will define the forward and backwards pass of your layer within the network. When caffe is prepared to pass data up to this layer, it will call the `Forward_cpu` or `Forward_gpu` method, in the case of running via the processor or the graphics card respectively. When caffe is performing back-propagation it will call the `Backward_cpu` or `Backward_gpu` method, in the case of running via the processor or the graphics card respectively.
 
     protected:
      virtual void Forward_cpu(const vector<Blob<Dtype>*>& bottom,
          const vector<Blob<Dtype>*>& top);
      virtual void Forward_gpu(const vector<Blob<Dtype>*>& bottom,
          const vector<Blob<Dtype>*>& top);

      virtual void Backward_cpu(const vector<Blob<Dtype>*>& top,
          const vector<bool>& propagate_down, const vector<Blob<Dtype>*>& bottom);
      virtual void Backward_gpu(const vector<Blob<Dtype>*>& top,
          const vector<bool>& propagate_down, const vector<Blob<Dtype>*>& bottom);

Completing the file.

    };
      
    }  // namespace caffe
    
    #endif  // CAFFE_SIN_LAYER_HPP_

### CPU Version

### GPU Version

### Testing Your Layer