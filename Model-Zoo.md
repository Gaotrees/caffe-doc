Check out the [model zoo documentation](http://caffe.berkeleyvision.org/model_zoo.html) for details.

To acquire a model:

1. download the model gist by `./scripts/download_model_from_gist.sh <gist_id> <dirname>` to load the model metadata, architecture, solver configuration, and so on. (`<dirname>` is optional and defaults to caffe/models).
2. download the model weights by `./scripts/download_model_binary.py <model_dir>` where `<model_dir>` is the gist directory from the first step.

or visit the [model zoo documentation](http://caffe.berkeleyvision.org/model_zoo.html) for complete instructions.

### Berkeley-trained models

 - [Finetuning on Flickr Style](https://gist.github.com/sergeyk/034c6ac3865563b69e60): same as provided in `models/`, but listed here as a Gist for an example.
 - BVLC GoogleNet: `models/bvlc_googlenet`

### Network in Network model
The Network in Network model is described in the following [ICLR-2014 paper](http://arxiv.org/abs/1312.4400):

    Network In Network
    M. Lin, Q. Chen, S. Yan
    International Conference on Learning Representations, 2014 (arXiv:1409.1556)

please cite the paper if you use the models.

Models:
 * [NIN-Imagenet](https://gist.github.com/mavenlin/d802a5849de39225bcc6): a small(29MB) model for imagenet, yet performs slightly better than AlexNet, and fast to train. (Note: a more caffe-compatible version with correct convolutional weights shape: https://drive.google.com/folderview?id=0B0IedYUunOQINEFtUi1QNWVhVVU&usp=drive_web)
 * [NIN-CIFAR10](https://gist.github.com/mavenlin/e56253735ef32c3c296d): NIN model on CIFAR10, originally published in the paper [Network In Network](http://arxiv.org/abs/1312.4400). The error rate of this model is 10.4% on CIFAR10.

### Models from the BMVC-2014 paper "Return of the Devil in the Details: Delving Deep into Convolutional Nets"

The models are trained on the ILSVRC-2012 dataset. The details can be found on the [project page](http://www.robots.ox.ac.uk/~vgg/research/deep_eval/) or in the following [BMVC-2014 paper](http://www.robots.ox.ac.uk/~vgg/publications/2014/Chatfield14/):

    Return of the Devil in the Details: Delving Deep into Convolutional Nets
    K. Chatfield, K. Simonyan, A. Vedaldi, A. Zisserman
    British Machine Vision Conference, 2014 (arXiv ref. cs1405.3531)

Please cite the paper if you use the models.

Models:
 * [VGG_CNN_S](https://gist.github.com/ksimonyan/fd8800eeb36e276cd6f9#file-readme-md): 13.1% top-5 error on ILSVRC-2012-val
 * [VGG_CNN_M](https://gist.github.com/ksimonyan/f194575702fae63b2829#file-readme-md): 13.7%  top-5 error on ILSVRC-2012-val
 * [VGG_CNN_M_2048](https://gist.github.com/ksimonyan/78047f3591446d1d7b91#file-readme-md): 13.5%  top-5 error on ILSVRC-2012-val
 * [VGG_CNN_M_1024](https://gist.github.com/ksimonyan/f0f3d010e6d5f0100274#file-readme-md): 13.7%  top-5 error on ILSVRC-2012-val
 * [VGG_CNN_M_128](https://gist.github.com/ksimonyan/976847408258292576a1#file-readme-md): 15.6%  top-5 error on ILSVRC-2012-val
 * [VGG_CNN_F](https://gist.github.com/ksimonyan/a32c9063ec8e1118221a#file-readme-md): 16.7%  top-5 error on ILSVRC-2012-val

### Models used by the VGG team in ILSVRC-2014

The models are the improved versions of the models used by the VGG team in the ILSVRC-2014 competition. The details can be found on the [project page](http://www.robots.ox.ac.uk/~vgg/research/very_deep/) or in the following [arXiv paper](http://arxiv.org/pdf/1409.1556):

    Very Deep Convolutional Networks for Large-Scale Image Recognition
    K. Simonyan, A. Zisserman
    arXiv:1409.1556

Please cite the paper if you use the models.

Models:
 * [16-layer](https://gist.github.com/ksimonyan/211839e770f7b538e2d8#file-readme-md): 7.5% top-5 error on ILSVRC-2012-val, 7.4% top-5 error on ILSVRC-2012-test
 * [19-layer](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77#file-readme-md): 7.5% top-5 error on ILSVRC-2012-val, 7.3% top-5 error on ILSVRC-2012-test

In the paper, the models are denoted as configurations `D` and `E`, trained with scale jittering.
The combination of the two models achieves 7.1% top-5 error on ILSVRC-2012-val, and 7.0% top-5 error on ILSVRC-2012-test.

### Places-CNN model from MIT.
Places CNN is described in the following [NIPS 2014 paper](http://places.csail.mit.edu/places_NIPS14.pdf):

    B. Zhou, A. Lapedriza, J. Xiao, A. Torralba, and A. Oliva
    Learning Deep Features for Scene Recognition using Places Database.
    Advances in Neural Information Processing Systems 27 (NIPS) spotlight, 2014.

The project page is [here](http://places.csail.mit.edu)

Models:
 * [Places205-AlexNet](http://places.csail.mit.edu/model/placesCNN.tar.gz): CNN trained on 205 scene categories of Places Database (used in NIPS'14) with ~2.5 million images. The architecture is the same as Caffe reference network.
 * [Hybrid-CNN](http://places.csail.mit.edu/model/hybridCNN.tar.gz): CNN trained on 1183 categories (205 scene categories from Places Database and 978 object categories from the train data of ILSVRC2012 (ImageNet) with ~3.6 million images. The architecture is the same as Caffe reference network.
 * [Places205-GoogLeNet](http://places.csail.mit.edu/model/googlenet_places205.tar.gz): GoogLeNet CNN trained on 205 scene categories of Places Database. It is used by Google in the [deep dream visualization](http://googleresearch.blogspot.com/2015/06/inceptionism-going-deeper-into-neural.html) 

### GoogLeNet GPU implementation from Princeton.
We implemented GoogLeNet using a single GPU. Our main contribution is an effective way to initialize the network and a trick to overcome the GPU memory constraint by accumulating gradients over two training iterations. 
* Please check [http://vision.princeton.edu/pvt/GoogLeNet/](http://vision.princeton.edu/pvt/GoogLeNet/) for more information. Pre-trained models on ImageNet and Places, and the training code are available for download.
* Make sure cls2_fc2 and cls3_fc have num_output = 1000 in the prototxt. Otherwise, the trained model would crash on test.

### <a name="fcn"></a>Fully Convolutional Semantic Segmentation Models (FCN-Xs)

These models are described in the [paper](http://cs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf):

    Fully Convolutional Models for Semantic Segmentation
    Jonathan Long, Evan Shelhamer, Trevor Darrell
    CVPR 2015
    arXiv:1411.4038

These are pre-release models. They do not run in any current version of BVLC/caffe, as they require unmerged PRs. They should run in the preview branch provided at https://github.com/longjon/caffe/tree/future. The [FCN-32s PASCAL-Context](https://gist.github.com/shelhamer/80667189b218ad570e82#file-readme-md) model is the most complete example including network definitions, solver configuration, and Python scripts for solving and inference.

Models trained on PASCAL (using extra data from [Hariharan et al.](http://www.cs.berkeley.edu/~bharath2/codes/SBD/download.html) and finetuned from the ILSVRC-trained VGG-16 model above):
* [FCN-32s PASCAL](https://gist.github.com/longjon/ac410cad48a088710872#file-readme-md): single stream, 32 pixel prediction stride version
* [FCN-16s PASCAL](https://gist.github.com/longjon/d24098e083bec05e456e#file-readme-md): two stream, 16 pixel prediction stride version
* [FCN-8s PASCAL](https://gist.github.com/longjon/1bf3aa1e0b8e788d7e1d#file-readme-md): three stream, 8 pixel prediction stride version
* [FCN-AlexNet PASCAL](https://gist.github.com/shelhamer/3f2c75f3c8c71357f24c#file-readme.md): AlexNet (CaffeNet) single stream, 32 pixel prediction stride version

To reproduce the validation scores, use the [seg11valid](https://gist.github.com/shelhamer/edb330760338892d511e) split defined by the paper in footnote 7. Since SBD train and PASCAL VOC 11 segval intersect, we only evaluate on the non-intersecting set for validation purposes.

Models trained on SIFT Flow (also finetuned from VGG-16):
* [FCN-16s SIFT Flow](https://gist.github.com/longjon/f35e3a101e1478f721f5#file-readme-md): two stream, 16 pixel prediction stride version

Models trained on NYUDv2 (also finetuned from VGG-16, and using HHA features from Gupta et al. https://github.com/s-gupta/rcnn-depth):
* [FCN-32s NYUDv2](https://gist.github.com/longjon/16db1e4ad3afc2614067#file-readme-md): single stream, 32 pixel prediction stride version
* [FCN-16s NYUDv2](https://gist.github.com/longjon/dd1f5097af6b531bddcc#file-readme-md): two stream, 16 pixel prediction stride version

Models trained on PASCAL-Context including training model definition, solver configuration, and barebones solving script (finetuned from the ILSVRC-trained VGG-16 model):
* [FCN-32s PASCAL-Context](https://gist.github.com/shelhamer/80667189b218ad570e82#file-readme-md): single stream, 32 pixel prediction stride version
* [FCN-16s PASCAL-Context](https://gist.github.com/shelhamer/08652f2ba191f64e619a#file-readme-md): two stream, 16 pixel prediction stride version
* [FCN-8s PASCAL-Context](https://gist.github.com/shelhamer/91eece041c19ff8968ee#file-readme-md): three stream, 8 pixel prediction stride version

### CaffeNet fine-tuned for Oxford flowers dataset
https://gist.github.com/jimgoo/0179e52305ca768a601f

The is the reference CaffeNet (modified [AlexNet](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)) fine-tuned for the [Oxford 102 category flower dataset](http://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html). The number of outputs in the inner product layer has been set to 102 to reflect the number of flower categories. Hyperparameter choices reflect those in [Fine-tuning CaffeNet for Style Recognition on “Flickr Style” Data](http://caffe.berkeleyvision.org/gathered/examples/finetune_flickr_style.html). The global learning rate is reduced while the learning rate for the final fully connected is increased relative to the other layers.

After 50,000 iterations, the top-1 error is 7% on the test set of 1,020 images.

```
I0215 15:28:06.417726  6585 solver.cpp:246] Iteration 50000, loss = 0.000120038
I0215 15:28:06.417789  6585 solver.cpp:264] Iteration 50000, Testing net (#0)
I0215 15:28:30.834987  6585 solver.cpp:315]     Test net output #0: accuracy = 0.9326
I0215 15:28:30.835072  6585 solver.cpp:251] Optimization Done.
I0215 15:28:30.835083  6585 caffe.cpp:121] Optimization Done.
```

### CNN Models for Salient Object Subitizing.
CNN models described in the following CVPR'15 papger "[Salient Object Subitizing](http://www.cs.bu.edu/groups/ivc/Subitizing/)":

    Salient Object Subitizing
    J. Zhang, S. Ma, M. Sameki, S. Sclaroff, M. Betke, Z. Lin, X. Shen, B. Price and R. Mech. 
    CVPR, 2015.

Models:
 * [AlexNet](https://gist.github.com/jimmie33/0585ed9428dc5222981f): CNN model finetuned on the Salient Object Subitizing dataset (~5500 images). The architecture is the same as the Caffe reference network.
 * [VGG16](https://gist.github.com/jimmie33/27c1c0a7736ba66c2395): CNN model finetuned on the Salient Object Subitizing dataset (~5500 images). The architecture is the same as the VGG16 network. This model gives better performance than the AlexNet model, but is slower for training and testing.

### Deep Learning of Binary Hash Codes for Fast Image Retrieval
We present an effective deep learning framework to create the hash-like binary codes for fast image retrieval. The details can be found in the following "[CVPRW'15 paper](http://www.iis.sinica.edu.tw/~kevinlin311.tw/cvprw15.pdf)":

    Deep Learning of Binary Hash Codes for Fast Image Retrieval
    K. Lin, H.-F. Yang, J.-H. Hsiao, C.-S. Chen
    CVPR 2015, DeepVision workshop

please cite the paper if you use the model:
 * [caffe-cvprw15](https://github.com/kevinlin311tw/caffe-cvprw15): See our code release on Github, which allows you to train your own deep hashing model and create binary hash codes.
 * [CIFAR10-48bit](https://gist.github.com/kevinlin311tw/266d4150a1db5810398e): Proposed 48-bits CNN model trained on CIFAR10.


### Places_CNDS_models on Scene Recognition

* [Places-CNDS-8](https://github.com/lwwang/Places_CNDS_model) is a "8conv3fc layer" deep Convolutional neural Networks model trained on MIT Places Dataset with Deep Supervision.

The details of training this model are described in the following [report](http://arxiv.org/pdf/1505.02496.pdf). Please cite this work if the model is useful for you.

    Training Deeper Convolutional Networks with Deep Supervision
    L.Wang, C.Lee, Z.Tu, S. Lazebnik, arXiv:1505.02496, 2015 


### Models for Age and Gender Classification.

* [Age/Gender.net](https://gist.github.com/GilLevi/c9e99062283c719c03de) are models for age and gender classification trained on the [Adience-OUI](http://www.openu.ac.il/home/hassner/Adience/data.html#agegender) dataset. See the [Project page](http://www.openu.ac.il/home/hassner/projects/cnn_agegender/). 

The models are described in the following paper:

    Gil Levi and Tal Hassner, Age and Gender Classification using Convolutional Neural Networks,
    IEEE Workshop on Analysis and Modeling of Faces and Gestures (AMFG),
    at the IEEE Conf. on Computer Vision and Pattern Recognition (CVPR), Boston, June 2015

If you find our models useful, please add suitable reference to our paper in your work.

### GoogLeNet_cars on car model classification
[GoogLeNet_cars](https://gist.github.com/bogger/b90eb88e31cd745525ae) is the GoogLeNet model pre-trained on ImageNet classification task and fine-tuned on 431 car models in [CompCars dataset](http://mmlab.ie.cuhk.edu.hk/datasets/comp_cars/index.html). It is described in the [technical report](http://arxiv.org/abs/1506.08959). Please cite the following work if the model is useful for you.

    A Large-Scale Car Dataset for Fine-Grained Categorization and Verification
    L. Yang, P. Luo, C. C. Loy, X. Tang, arXiv:1506.08959, 2015

### <a name="parsenet"></a>ParseNet: Looking wider to see better

These models are described in the [paper](http://arxiv.org/abs/1506.04579):

    ParseNet: Looking Wider to See Better
    Wei Liu, Andrew Rabinovich, Alexander C. Berg
    arXiv:1506.04579

To be able to train/eval ParseNet, you can refer to http://github.com/weiliu89/caffe/tree/fcn.

Modified VGGNet used to fine-tune ParseNet:

 * [fully convolutional reduced VGGNet](https://gist.github.com/weiliu89/2ed6e13bfd5b57cf81d6)

Models trained on PASCAL (using extra data from [Hariharan et al.](http://www.cs.berkeley.edu/~bharath2/codes/SBD/download.html) and finetuned from the [fully convolutional reduced VGGNet](https://gist.github.com/weiliu89/2ed6e13bfd5b57cf81d6)):

 * [ParseNet PASCAL](https://gist.github.com/weiliu89/45e9e8de2c13af6476ca#file-readme-md)

### <a name="crfasrnn"></a>Conditional Random Fields as Recurrent Neural Networks

Code (with Matlab/Python API) and model are described in the ICCV 2015 [paper](http://www.robots.ox.ac.uk/~szheng/papers/CRFasRNN.pdf)

    Conditional Random Fields as Recurrent Neural Networks
    S. Zheng, S. Jayasumana, B. Romera-Paredes, V. Vineet, Z. Su, D. Du, C. Huang, P. Torr
    ICCV 2015.

Model is trained on Microsoft COCO and PASCAL (using extra data from [Hariharan et al.](http://www.cs.berkeley.edu/~bharath2/codes/SBD/download.html) 
and finetuned from the [FCN-8s](https://gist.github.com/longjon/1bf3aa1e0b8e788d7e1d)):

 * [CRF-RNN PASCAL](https://github.com/torrvision/crfasrnn)

### <a name="hed"></a>Holistically-Nested Edge Detection

The model and code provided are described in the ICCV 2015 [paper](http://arxiv.org/abs/1504.06375):

    Holistically-Nested Edge Detection
    Saining Xie and Zhuowen Tu
    ICCV 2015

For details about training/evaluating HED, please take a look at http://github.com/s9xie/hed.

Model trained on BSDS-500 Dataset (finetuned from the VGGNet):

 * [HED BSDS-500](https://gist.github.com/s9xie/c6bd432f7347548b0187)

###Translating Videos to Natural Language 

These models are described in [this NAACL-HLT 2015 paper](http://www.cs.utexas.edu/users/ml/papers/venugopalan.naacl15.pdf).  

    Translating Videos to Natural Language Using Deep Recurrent Neural Networks 
    S. Venugopalan, H. Xu, J. Donahue, M. Rohrbach, R. Mooney, K. Saenko   
    NAACL-HLT 2015
                                                                           
More details can be found on [this project 
page](https://www.cs.utexas.edu/~vsub/naacl15_project.html).               

Model:                                                                     
[Video2Text_VGG_mean_pool](https://gist.github.com/vsubhashini/3761b9ad43f60db9ac3d): 
This model is an improved version of the mean pooled model described in the NAACL-HLT 2015 paper. It uses video frame features from the
[VGG-16](https://gist.github.com/ksimonyan/211839e770f7b538e2d8#file-readme-md) layer model. This is trained only on the Youtube video dataset.       
                                                                           
Compatibility:
These are pre-release models. They do not run in any current version of BVLC/caffe, as they require unmerged PRs. The models are currently supported  by the `recurrent` branch of the Caffe fork provided at https://github.com/jeffdonahue/caffe/tree/recurrent and https://github.com/vsubhashini/caffe/tree/recurrent.


###VGG Face CNN descriptor

These models are described in this [BMVC 2015 paper] (http://www.robots.ox.ac.uk/~vgg/publications/2015/Parkhi15/parkhi15.pdf).  

    Deep Face Recognition 
    Omkar M. Parkhi, Andrea Vedaldi, Andrew Zisserman    
    BMVC 2015

                                                                     
More details can be found on [this project 
page](http://www.robots.ox.ac.uk/~vgg/software/vgg_face/).

Model:
[VGG Face](http://www.robots.ox.ac.uk/~vgg/software/vgg_face/src/vgg_face_caffe.tar.gz):
This is the very deep architecture based model trained from scratch using 2.6 Million images
of celebrities collected from the web. The model has been imported to work with Caffe from the 
original model trained using MatConvNet library.  

If you find our models useful, please add suitable reference to our paper in your work.

###Yearbook Photo Dating
Model from the [ICCV 2015 Extreme Imaging Workshop paper](http://arxiv.org/abs/1511.02575):

    A Century of Portraits: Exploring the Visual Historical Record of American High School Yearbooks 
    Shiry Ginosar, Kate Rakelly, Brian Yin, Sarah Sachs, Alyosha Efros
    ICCV Workshop 2015

Model and prototxt files: [Yearbook](https://gist.github.com/katerakelly/842f948d568d7f1f0044)

### <a name="ccnn"></a>CCNN: Constrained Convolutional Neural Networks for Weakly Supervised Segmentation

These models are described in the [ICCV 2015 paper](http://arxiv.org/abs/1506.03648).

    Constrained Convolutional Neural Networks for Weakly Supervised Segmentation
    Deepak Pathak, Philipp Krähenbühl, Trevor Darrell
    ICCV 2015
    arXiv:1506.03648

These are pre-release models. They do not run in any current version of BVLC/caffe, as they require unmerged PRs.
Full details, source code, models, prototxts are available here: [CCNN](https://github.com/pathak22/ccnn).