## Projects Using Caffe

**Fast R-CNN** is a fast framework for object detection with deep ConvNets. Fast R-CNN
 - trains state-of-the-art models, like VGG16, 9x faster than traditional R-CNN and 3x faster than SPPnet,
 - runs 200x faster than R-CNN and 10x faster than SPPnet at test-time,
 - has a significantly higher mAP on PASCAL VOC than both R-CNN and SPPnet,
 - and is written in Python and C++/Caffe.

Please take a look at @rbgirshick work at https://github.com/rbgirshick/fast-rcnn

***
![Expresso screenshot](http://val.serc.iisc.ernet.in/expresso/main-screen.png)
**Expresso** is a Python-based GUI for designing, training and using CNNs. Expresso uses Caffe as its backend CNN framework. Some of its salient features : 
 - A convenient wizard-like interface to contextually guide the user during common scenarios
such as data import, design and training of CNNs
 - A smart-edit interface makes net creation easy and quick. 
 - Deep networks are color-coded and informatively presented
 - Support for training external classifier (SVM) using deep features (i.e. features extracted by passing image data through pre-trained CNN and tapping output at layer(s) of CNN).
 - Data Visualization

Visit the [project page](http://val.serc.iisc.ernet.in/expresso) for installation details and links to text/video tutorials.

## Other Useful Components

* Fast object proposal LPO by @philkr https://github.com/philkr/lpo
* Look [here](https://pdollar.wordpress.com/2014/11/18/evaluating-object-proposals/) for other object proposal other then selective search.