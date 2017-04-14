## Projects Using Caffe

**Fast R-CNN** is a fast framework for object detection with deep ConvNets. Fast R-CNN
 - trains state-of-the-art models, like VGG16, 9x faster than traditional R-CNN and 3x faster than SPPnet,
 - runs 200x faster than R-CNN and 10x faster than SPPnet at test-time,
 - has a significantly higher mAP on PASCAL VOC than both R-CNN and SPPnet,
 - and is written in Python and C++/Caffe.

Please take a look at @rbgirshick work at https://github.com/rbgirshick/fast-rcnn

***

The [Facebook Caffe Extensions](https://github.com/facebook/fb-caffe-exts) include the `predictor` inference API, a `torch2caffe` translator, and other conversion scripts and tools. Thanks to @ajtulloch.

***

The [NVIDIA GPU Rest Engine](https://github.com/NVIDIA/gpu-rest-engine) demonstrates a server for low-latency image classification inference. It is a technical demo that shows how you can add a REST API on top of Caffe using the Go language, and how to package all your dependencies inside a Docker container. Thanks to @flx42.

***

[Ristretto](http://lepsucd.com/?page_id=621) is a framework for deep network approximation that can help experiment with quantization, reduced precision, and other optimizations.

***

***
![Expresso screenshot](http://val.serc.iisc.ernet.in/expresso/main-screen.png)
**[Expresso](https://github.com/val-iisc/expresso)** is a Python-based GUI for designing, training and using CNNs. Expresso uses Caffe as its backend CNN framework. Some of its salient features : 
 - A convenient wizard-like interface to contextually guide the user during common scenarios
such as data import, design and training of CNNs
 - A smart-edit interface makes net creation easy and quick. 
 - Deep networks are color-coded and informatively presented
 - Support for training external classifier (SVM) using deep features (i.e. features extracted by passing image data through pre-trained CNN and tapping output at layer(s) of CNN).
 - Data Visualization

Visit the [project page](http://val.serc.iisc.ernet.in/expresso) for installation details and links to text/video tutorials.

***

**Deep Visualization Toolbox** is an open source software tool that lets you probe deep networks by feeding them an image (or a live webcam feed) and watching the reaction of every unit. You can also select individual units to view pre-rendered visualizations of what that neuron “wants to see most”.

Visit the [deep-vis project page](http://yosinski.com/deepvis) and the @yosinski project at https://github.com/yosinski/deep-visualization-toolbox

***

**Caffe with Spearmint** integrates the deep learning framework with spearmint bayesian hyperparamter optimization to automate parameter search.

Visit the @kuz project at https://github.com/kuz/caffe-with-spearmint

## Other Useful Components

* Fast object proposal LPO by @philkr https://github.com/philkr/lpo
* Look [here](https://pdollar.wordpress.com/2014/11/18/evaluating-object-proposals/) for other object proposal other then selective search.