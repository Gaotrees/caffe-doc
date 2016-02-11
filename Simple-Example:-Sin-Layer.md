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

Basic file setup.

    // Sin neuron activation function layer.
    // Adapted from TanH layer which was adapted from the ReLU layer code written by Yangqing Jia
    
    #include <vector>
    
    #include "caffe/layers/sin_layer.hpp"
    
    namespace caffe {
    
When it is our layer's turn to process the data, caffe will call the `Forward_cpu` method. The forward step takes data in from the `bottom` (a previous layer generally) via an array of Blobs. In this layer we will be transforming the data via a `sin` function. 

We take in an immutable reference of the bottom (what our layer will be getting input from), and a mutable reference to the top (what our layer will be outputting to). We will transform the input data and store it in the output. That's it!

    template <typename Dtype>
    void SinLayer<Dtype>::Forward_cpu(const vector<Blob<Dtype>*>& bottom,
                                      const vector<Blob<Dtype>*>& top) 
    { 
      const Dtype* bottom_data = bottom[0]->cpu_data();
      Dtype* top_data = top[0]->mutable_cpu_data();
      const int count = bottom[0]->count();
      for (int i = 0; i < count; ++i) {
        top_data[i] = sin(bottom_data[i]);
      }
    }

When it is our layer's turn to calculate the gradient (the effect we've had on the loss function), caffe will call the `Backward_cpu` method. The backward step takes data in from the `top` (a previous layer generally) via an array of Blobs. In this layer we will be, in part, calculating the loss with respect to this layer via the derivative of the `sin` function - the `cos` function. 

We take in an immutable reference of the bottom (what our layer had previously received input from), an immutable copy of the derivative from the layer above us, and a mutable reference to the gradient that we will output. We calculate the gradient, applying the chain rule (a multiplication with the previous calculation), and set the output gradient (`bottom_diff`).

    template <typename Dtype>
    void SinLayer<Dtype>::Backward_cpu(const vector<Blob<Dtype>*>& top,
                                        const vector<bool>& propagate_down,
                                        const vector<Blob<Dtype>*>& bottom) 
    { 
      if (propagate_down[0]) {
        const Dtype* bottom_data = bottom[0]->cpu_data();
        const Dtype* top_diff = top[0]->cpu_diff();
        Dtype* bottom_diff = bottom[0]->mutable_cpu_diff();
        const int count = bottom[0]->count();
        Dtype top_datum;
        for (int i = 0; i < count; ++i) {
          bottom_datum = bottom_data[i];
          bottom_diff[i] = top_diff[i] * cos(bottom_datum);
        }
      }
    }

Closing off the class.
    
    #ifdef CPU_ONLY
    STUB_GPU(SinLayer);
    #endif
    
    INSTANTIATE_CLASS(SinLayer);
    REGISTER_LAYER_CLASS(Sin);
    
    }  // namespace caffe    

### GPU Version

Basic file setup.

    // Sin neuron activation function layer.
    // Adapted from TanH layer which was adapted from the ReLU layer code written by Yangqing Jia
    
    #include <vector>
    
    #include "caffe/layers/sin_layer.hpp"
    
    namespace caffe {

When it is our layer's turn to process the data, caffe will call the `Forward_gpu` method. The forward step takes data in from the `bottom` (a previous layer generally) via an array of Blobs. In this layer we will be transforming the data via a `sin` function. 

We take in an immutable reference of the bottom (what our layer will be getting input from), and a mutable reference to the top (what our layer will be outputting to). We will transform the input data and store it in the output. That's it!

    template <typename Dtype>
    __global__ void SinForward(const int n, const Dtype* in, Dtype* out) {
      CUDA_KERNEL_LOOP(index, n) {
        out[index] = sin(in[index]);
      }
    }
    
    template <typename Dtype>
    void SinLayer<Dtype>::Forward_gpu(const vector<Blob<Dtype>*>& bottom,
        const vector<Blob<Dtype>*>& top) {
      const Dtype* bottom_data = bottom[0]->gpu_data();
      Dtype* top_data = top[0]->mutable_gpu_data();
      const int count = bottom[0]->count();
      // NOLINT_NEXT_LINE(whitespace/operators)
      SinForward<Dtype><<<CAFFE_GET_BLOCKS(count), CAFFE_CUDA_NUM_THREADS>>>(
          count, bottom_data, top_data);
      CUDA_POST_KERNEL_CHECK;
    }

When it is our layer's turn to calculate the gradient (the effect we've had on the loss function), caffe will call the `Backward_cpu` method. The backward step takes data in from the `top` (a previous layer generally) via an array of Blobs. In this layer we will be, in part, calculating the loss with respect to this layer via the derivative of the `sin` function - the `cos` function. 

We take in an immutable reference of the bottom (what our layer had previously received input from), an immutable copy of the derivative from the layer above us, and a mutable reference to the gradient that we will output. We calculate the gradient, applying the chain rule (a multiplication with the previous calculation), and set the output gradient (`bottom_diff`).

    template <typename Dtype>
    __global__ void SinBackward(const int n, const Dtype* in_diff,
        const Dtype* out_data, Dtype* out_diff) {
      CUDA_KERNEL_LOOP(index, n) {
        Dtype sinx = out_data[index];
        out_diff[index] = in_diff[index] * cos(sinx);
      }
    }
    
    template <typename Dtype>
    void SinLayer<Dtype>::Backward_gpu(const vector<Blob<Dtype>*>& top,
        const vector<bool>& propagate_down,
        const vector<Blob<Dtype>*>& bottom) {
      if (propagate_down[0]) {
        const Dtype* bottom_data = bottom[0]->gpu_data();
        const Dtype* top_diff = top[0]->gpu_diff();
        Dtype* bottom_diff = bottom[0]->mutable_gpu_diff();
        const int count = bottom[0]->count();
        // NOLINT_NEXT_LINE(whitespace/operators)
        SinBackward<Dtype><<<CAFFE_GET_BLOCKS(count), CAFFE_CUDA_NUM_THREADS>>>(
            count, top_diff, bottom_data, bottom_diff);
        CUDA_POST_KERNEL_CHECK;
      }
    }

Closing off the class.
    
    INSTANTIATE_LAYER_GPU_FUNCS(SinLayer);
    
    
    }  // namespace caffe

### Testing Your Layer

Basic file setup.

    #include <algorithm>
    #include <vector>
    
    #include "gtest/gtest.h"
    
    #include "caffe/blob.hpp"
    #include "caffe/common.hpp"
    #include "caffe/filler.hpp"
    
    #include "caffe/test/test_caffe_main.hpp"
    #include "caffe/test/test_gradient_check_util.hpp"

Include the layer that we are testing!
    
   #include "caffe/layers/sin_layer.hpp"

More file setup.

    namespace caffe {
    
    template <typename TypeParam>
    class SinLayerTest : public MultiDeviceTest<TypeParam> {
      typedef typename TypeParam::Dtype Dtype;
    
     protected:
      SinLayerTest()
          : blob_bottom_(new Blob<Dtype>(2, 3, 4, 5)),
            blob_top_(new Blob<Dtype>())
      {
        Caffe::set_random_seed(1701);
        FillerParameter filler_param;
        blob_bottom_vec_.push_back(blob_bottom_);
        blob_top_vec_.push_back(blob_top_);
      }
      virtual ~SinLayerTest() { delete blob_bottom_; delete blob_top_; }
 
This is a helper method that will be used to calculate the forward data transformation of the network as it calls upon our layer.
   
        void TestForward(Dtype filler_std)
      {
        FillerParameter filler_param;
        filler_param.set_std(filler_std);
        GaussianFiller<Dtype> filler(filler_param);
        filler.Fill(this->blob_bottom_);
    
        LayerParameter layer_param;
        SinLayer<Dtype> layer(layer_param);
        layer.SetUp(this->blob_bottom_vec_, this->blob_top_vec_);
        layer.Forward(this->blob_bottom_vec_, this->blob_top_vec_);
        // Now, check values
        const Dtype* bottom_data = this->blob_bottom_->cpu_data();
        const Dtype* top_data = this->blob_top_->cpu_data();
        const Dtype min_precision = 1e-5;
        for (int i = 0; i < this->blob_bottom_->count(); ++i) {
          Dtype expected_value = sin(bottom_data[i]);
          Dtype precision = std::max(
            Dtype(std::abs(expected_value * Dtype(1e-4))), min_precision);
          EXPECT_NEAR(expected_value, top_data[i], precision);
        }
      }
    
This is a helper method that will be used to calculate the gradient calculation on the backwards pass of the network through our layer.

      void TestBackward(Dtype filler_std)
      {
        FillerParameter filler_param;
        filler_param.set_std(filler_std);
        GaussianFiller<Dtype> filler(filler_param);
        filler.Fill(this->blob_bottom_);
    
        LayerParameter layer_param;
        SinLayer<Dtype> layer(layer_param);
        GradientChecker<Dtype> checker(1e-4, 1e-2, 1701);
        checker.CheckGradientEltwise(&layer, this->blob_bottom_vec_,
            this->blob_top_vec_);
      }
    
      Blob<Dtype>* const blob_bottom_;
      Blob<Dtype>* const blob_top_;
      vector<Blob<Dtype>*> blob_bottom_vec_;
      vector<Blob<Dtype>*> blob_top_vec_;
    };

I don't know what this does yet.
    
    TYPED_TEST_CASE(SinLayerTest, TestDtypesAndDevices);

Here we will be defining a test, with the test set name `SinLayerTest` (naming convention for grouping tests), and a descriptive unique test name `TestSin`.
    
    TYPED_TEST(SinLayerTest, TestSin) {
      this->TestForward(1.0);
    }

A descriptive unique test name `TestSinGradient`, that will test that our layer is calculating the gradient correctly when backpragating.

    TYPED_TEST(SinLayerTest, TestSinGradient) {
      this->TestBackward(1.0);
    }

Closing the file.

    }  // namespace caffe