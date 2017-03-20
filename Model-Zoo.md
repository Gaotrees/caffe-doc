Check out the [model zoo documentation](http://caffe.berkeleyvision.org/model_zoo.html) for details.

To acquire a model:

1. download the model gist by `./scripts/download_model_from_gist.sh <gist_id> <dirname>` to load the model metadata, architecture, solver configuration, and so on. (`<dirname>` is optional and defaults to caffe/models).
2. download the model weights by `./scripts/download_model_binary.py <model_dir>` where `<model_dir>` is the gist directory from the first step.

or visit the [model zoo documentation](http://caffe.berkeleyvision.org/model_zoo.html) for complete instructions.

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Berkeley-trained models](#berkeley-trained-models)
- [Network in Network model](#network-in-network-model)
- [Models from the BMVC-2014 paper "Return of the Devil in the Details: Delving Deep into Convolutional Nets"](#models-from-the-bmvc-2014-paper-return-of-the-devil-in-the-details-delving-deep-into-convolutional-nets)
- [Models used by the VGG team in ILSVRC-2014](#models-used-by-the-vgg-team-in-ilsvrc-2014)
- [Places-CNN model from MIT.](#places-cnn-model-from-mit)
- [GoogLeNet GPU implementation from Princeton.](#googlenet-gpu-implementation-from-princeton)
- [Fully Convolutional Networks for Semantic Segmentation (FCNs)](#fully-convolutional-networks-for-semantic-segmentation-fcns)
- [CaffeNet fine-tuned for Oxford flowers dataset](#caffenet-fine-tuned-for-oxford-flowers-dataset)
- [CNN Models for Salient Object Subitizing.](#cnn-models-for-salient-object-subitizing)
- [Deep Learning of Binary Hash Codes for Fast Image Retrieval](#deep-learning-of-binary-hash-codes-for-fast-image-retrieval)
- [Places_CNDS_models on Scene Recognition](#placescndsmodels-on-scene-recognition)
- [Models for Age and Gender Classification.](#models-for-age-and-gender-classification)
- [GoogLeNet_cars on car model classification](#googlenetcars-on-car-model-classification)
- [ParseNet: Looking wider to see better](#parsenet-looking-wider-to-see-better)
- [SegNet and Bayesian SegNet](#segnet-and-bayesian-segnet)
- [Conditional Random Fields as Recurrent Neural Networks](#conditional-random-fields-as-recurrent-neural-networks)
- [Holistically-Nested Edge Detection](#holistically-nested-edge-detection)
- [CCNN: Constrained Convolutional Neural Networks for Weakly Supervised Segmentation](#ccnn-constrained-convolutional-neural-networks-for-weakly-supervised-segmentation)
- [Emotion Recognition in the Wild via Convolutional Neural Networks and Mapped Binary Patterns](#emotion-recognition-in-the-wild-via-convolutional-neural-networks-and-mapped-binary-patterns)
- [Facial Landmark Detection with Tweaked Convolutional Neural Networks](#facial-landmark-detection-with-tweaked-convolutional-neural-networks)
- [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](#faster-r-cnn-towards-real-time-object-detection-with-region-proposal-networks)
- [ResNets: Deep Residual Networks from MSRA at ImageNet and COCO 2015](#resnets-deep-residual-networks-from-msra-at-imagenet-and-coco-2015)
- [Pascal VOC 2012 Multilabel Classification Model](#pascal-voc-2012-multilabel-classification-model)
- [SqueezeNet: AlexNet-level accuracy with 50x fewer parameters](#squeezenet-alexnet-level-accuracy-with-50x-fewer-parameters)
- [Mixture DCNN](#mixture-dcnn)
- [CNN Object Proposal Models for Salient Object Detection](#cnn-object-proposal-models-for-salient-object-detection)
- [Deep Hand: How to Train a CNN on 1 Million Hand Images When Your Data Is Continuous and Weakly Labelled](#deep-hand-how-to-train-a-cnn-on-1-million-hand-images-when-your-data-is-continuous-and-weakly-labelled)
- [Mulimodal Compact Bilinear Pooling for VQA](#mulimodal-compact-bilinear-pooling-for-vqa)
- [Pose-Aware CNN Models (PAMs) for Face Recognition](#pose-aware-cnn-models-pams-for-face-recognition)
- [Learning Structured Sparsity in Deep Neural Networks](#learning-structured-sparsity-in-deep-neural-networks)
- [Neural Activation Constellations: Unsupervised Part Model Discovery with Convolutional Networks](#neural-activation-constellations-unsupervised-part-model-discovery-with-convolutional-networks)
- [Inception-BN full ImageNet model](#inception-bn-full-imagenet-model)
- [ResNet-101 for Face Recognition](#resnet-101-for-face-recognition)
- [DeepYeast](#deepyeast)
- [ImageNet pre-trained models with batch normalization](#imagenet-pre-trained-models-with-batch-normalization)
- [ResNet-101 for regressing 3D morphable face models (3DMM) from single images](#resnet-101-for-regressing-3d-morphable-face-models-3dmm-from-single-images)
- [Cascaded Fully Convolutional Networks for Biomedical Image Segmentation](#cascaded-fully-convolutional-networks-for-biomedical-image-segmentation)
- [Deep Networks for Earth Observation](#deep-networks-for-earth-observation)
- [Supervised Learning of Semantics-Preserving Hash via Deep Convolutional Neural Networks](#supervised-learning-of-semantics-preserving-hash-via-deep-convolutional-neural-networks)
- [Striving for Simplicity: The All Convolutional Net](#striving-for-simplicity-the-all-convolutional-net)

<!-- markdown-toc end -->

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
[![Try model on Haystack](https://img.shields.io/badge/try-on%20haystack-blue.svg)](https://www.haystack.ai/demos/Places205-AlexNet-Demo)

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

### <a name="fcn"></a>Fully Convolutional Networks for Semantic Segmentation (FCNs)

These models are described in the [paper](http://cs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf):

    Fully Convolutional Models for Semantic Segmentation
    Jonathan Long*, Evan Shelhamer*, Trevor Darrell
    CVPR 2015
    arXiv:1411.4038

Details, model definitions, pre-trained weights, and code are public on github: https://github.com/shelhamer/fcn.berkeleyvision.org.

These models are compatible with Caffe master, unlike earlier FCNs that required a pre-release branch (note: this reference edition of the models is still in progress and not all of the models have yet been ported to master). The models are available under the same license as the Caffe-bundled models (i.e., for unrestricted use; see http://caffe.berkeleyvision.org/model_zoo.html#bvlc-model-license).

### CaffeNet fine-tuned for Oxford flowers dataset
[![Try model on Haystack](https://img.shields.io/badge/try-on%20haystack-blue.svg)](https://www.haystack.ai/demos/Oxford-Flower-Demo)

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
CNN subitizing models described in the following papers ([project page](http://www.cs.bu.edu/groups/ivc/Subitizing/)):

    Salient Object Subitizing
    J. Zhang, S. Ma, M. Sameki, S. Sclaroff, M. Betke, Z. Lin, X. Shen, B. Price and R. Mech.
    CVPR, 2015.
    http://cs-people.bu.edu/jmzhang/SOS/SOS_preprint.pdf

    Salient Object Subitizing
    J. Zhang, S. Ma, M. Sameki, S. Sclaroff, M. Betke, Z. Lin, X. Shen, B. Price and R. Mech.
    arXiv, 2016.
    http://arxiv.org/abs/1607.07525

Models:
 * [GoogleNet](https://gist.github.com/jimmie33/7ea9f8ac0da259866b854460f4526034): CNN model finetuned on the Extended Salient Object Subitizing dataset (~11K images) and synthetic images. This model significantly improves over our previous models. **Recommended**.
 * [AlexNet](https://gist.github.com/jimmie33/0585ed9428dc5222981f): CNN model finetuned on our initial Salient Object Subitizing dataset (~5500 images). The architecture is the same as the Caffe reference network.
 * [VGG16](https://gist.github.com/jimmie33/27c1c0a7736ba66c2395): CNN model finetuned on our initial Salient Object Subitizing dataset (~5500 images). 

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

    Age and Gender Classification using Convolutional Neural Networks
    Gil Levi and Tal Hassner
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

### <a name="segnet"></a>SegNet and Bayesian SegNet

SegNet is a real-time semantic segmentation architecture for scene understanding. Code and trained models for [SegNet](http://arxiv.org/abs/1511.00561) and [Bayesian SegNet](http://arxiv.org/abs/1511.02680) are available.

    SegNet: A Deep Convolutional Encoder-Decoder Architecture for Image Segmentation
    Vijay Badrinarayanan, Alex Kendall and Roberto Cipolla
    arXiv preprint arXiv:1511.00561, 2015.

 * [Code](https://github.com/alexgkendall/caffe-segnet)
 * [Tutorial](http://mi.eng.cam.ac.uk/projects/segnet/)

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
[![Try model on Haystack](https://img.shields.io/badge/try-on%20haystack-blue.svg)](https://www.haystack.ai/demos/Yearbook-Demo)

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

### Emotion Recognition in the Wild via Convolutional Neural Networks and Mapped Binary Patterns

We provide [models](https://gist.github.com/GilLevi/54aee1b8b0397721aa4b) for facial emotion classification for different image representation obtained using mapped binary patterns. See the [Project page](http://www.openu.ac.il/home/hassner/projects/cnn_emotions/) for more details. 

The models are described in the following paper:

    Emotion Recognition in the Wild via Convolutional Neural Networks and Mapped Binary Patterns
    Gil Levi and Tal Hassner
    Proc. ACM International Conference on Multimodal Interaction (ICMI), Seattle, Nov. 2015

If you find our models useful, please add suitable reference to our paper in your work.

### Facial Landmark Detection with Tweaked Convolutional Neural Networks
We provide [source code](http://bit.ly/gtvnl2b) and [model](http://bit.ly/1ni6lpS) for article:
Yue Wu and Tal Hassner, "Facial Landmark Detection with Tweaked Convolutional Neural Networks", arXiv preprint arXiv:1511.04031, 12 Nov. 2015. 
See [project page](http://www.openu.ac.il/home/hassner/projects/tcnn_landmarks/) for more information about this project.

Written by [Ishay Tubi](https://www.linkedin.com/in/ishay2b)

This software is provided as is, without any warranty, with no legal constraints.
If you find our models useful, please add suitable reference to our paper in your work.

### Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks

Download pre-computed Faster R-CNN detectors
cd $FRCN_ROOT  
./data/scripts/fetch_faster_rcnn_models.sh
This will populate the $FRCN_ROOT/data folder with faster_rcnn_models. See data/README.md for details. These models were trained on VOC 2007 trainval.

ref  https://github.com/rbgirshick/py-faster-rcnn/blob/master/data/scripts/fetch_faster_rcnn_models.sh

###Sequence to Sequence - Video to Text                                                                                                                                                         
                                                                                                                                                                                                
These models are described in [this ICCV 2015 paper](http://www.cs.utexas.edu/users/ml/papers/venugopalan.iccv15.pdf).                                                                          
                                                                                                                                                                                                
    Sequence to Sequence - Video to Text
    S. Venugopalan, M. Rohrbach, J. Donahue, T. Darrell, R. Mooney, K. Saenko
    The IEEE International Conference on Computer Vision (ICCV) 2015
                                                                                                                                                                                                
More details can be found on [this project page](https://vsubhashini.github.io/s2vt.html).
                                                                                                                               
Model:                                                                                                                                                                                          
[S2VT_VGG_RGB](https://gist.github.com/vsubhashini/38d087e140854fee4b14):                                                                                                                       
This is the S2VT (RGB) model described in the ICCV 2015 paper. It uses video frame features from the                                                                                            [VGG-16](https://gist.github.com/ksimonyan/211839e770f7b538e2d8#file-readme-md) layer model. This is trained only on the Youtube video dataset.

Compatibility:                                                                                                                                                                                  
These are pre-release models. They do not run in any current version of BVLC/caffe, as they require unmerged PRs. The models are currently supported  by the `recurrent` branch of the Caffe    fork provided at https://github.com/jeffdonahue/caffe/tree/recurrent and https://github.com/vsubhashini/caffe/tree/recurrent.


### ResNets: Deep Residual Networks from MSRA at ImageNet and COCO 2015

This repository contains the original models (ResNet-50, ResNet-101, and ResNet-152) described in the paper "Deep Residual Learning for Image Recognition" (http://arxiv.org/abs/1512.03385). These models are those used in [ILSVRC] (http://image-net.org/challenges/LSVRC/2015/) and [COCO](http://mscoco.org/dataset/#detections-challenge2015) 2015 competitions, which won the 1st places in: ImageNet classification, ImageNet detection, ImageNet localization, COCO detection, and COCO segmentation.

More instructions with prototxt and binary weight files are in: https://github.com/KaimingHe/deep-residual-networks

Reference:

	@article{He2015,
		author = {Kaiming He and Xiangyu Zhang and Shaoqing Ren and Jian Sun},
		title = {Deep Residual Learning for Image Recognition},
		journal = {arXiv preprint arXiv:1512.03385},
		year = {2015}
	}



### Pascal VOC 2012 Multilabel Classification Model

This model has been used for the paper "Analyzing Classifiers: Fisher Vectors and Deep Neural Networks" (http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Bach_Analyzing_Classifiers_Fisher_CVPR_2016_paper.pdf), published in the proceedings of CVPR 2016.
Kindly note, that it has been trained in a multilabel setting with a multilabel-compatible loss function. It should not be used in conjunction with a softmax layer
In particular $f_{i}(x)>0$ denotes presence of class i and multiple classes can be predicted in one image.

Downloading the Model: [caffemodel](http://heatmapping.org/files/bvlc_model_zoo/pascal_voc_2012_multilabel/pascalvoc2012_train_simple2_iter_30000.caffemodel) [prototxt](http://heatmapping.org/files/bvlc_model_zoo/pascal_voc_2012_multilabel/deploy_x30.prototxt)

Please reference the above submission when using the model via

    @inproceedings{lapuschkinCVPR16,
        title={Analyzing classifiers: Fisher vectors and deep neural networks},
        author={Lapuschkin, S. and Binder, A. and Montavon, G. and M{\"u}ller, K.-R. and Samek, W.},
        booktitle={CVPR},
        pages={2912-2920},
        year={2016}
    }

### SqueezeNet: AlexNet-level accuracy with 50x fewer parameters

    @article{SqueezeNet,
        Author = {Forrest N. Iandola and Matthew W. Moskewicz and Khalid Ashraf and Song Han and William J. Dally and Kurt Keutzer},
        Title = {SqueezeNet: AlexNet-level accuracy with 50x fewer parameters and $<$1MB model size},
        Journal = {arXiv:1602.07360},
        Year = {2016}
    }

Please cite the paper if you use the model.

[**Model** trained on ImageNet](https://github.com/DeepScale/SqueezeNet) (including weights, solver, train_val, and deploy prototxt files)
* Error rate on ImageNet ILSVRC-2012 is better than or equal to the `bvlc_alexnet` model. 

### <a name="mixdcnn"></a>Mixture DCNN

Mixture DCNN is a novel multi-model architecture which achieves better performance than an ensemble of DCNNs as evaluated on three different fine-grained datasets. Please cite the following paper if you use these models in your research.

    @inproceedings{GeWACV2016,
      author    = {ZongYuan Ge and Alex Bewley and Christopher McCool and Ben Upcroft and Peter Corke and Conrad Sanderson},
      title     = {Fine-Grained Classification via Mixture of Deep Convolutional Neural Networks},
      booktitle = {Winter Conference on the Applications of Computer Vision (WACV)},
      publisher = {IEEE},
      year      = {2016}
    }

 * [Models](https://github.com/zongyuange/MixDCNN)
 * [Paper](http://arxiv.org/abs/1511.09209)

### CNN Object Proposal Models for Salient Object Detection

CNN models for the following CVPR'16 paper: 

    Unconstrained Salient Object Detection via Proposal Subset Optimization
    J. Zhang, S. Sclaroff, Z. Lin, X. Shen, B. Price and R. Mech. 
    CVPR, 2016.
    
[[PDF](http://cs-people.bu.edu/jmzhang/SOD/CVPR16SOD_camera_ready.pdf)] 
[[Webpage](http://cs-people.bu.edu/jmzhang/sod.html)]

The following models are finetuned on [the Salient Object Subitizing dataset](http://cs-people.bu.edu/jmzhang/sos.html) (~5000 images) with bounding box annotations:
 * [VGG16](https://gist.github.com/jimmie33/509111f8a00a9ece2c3d5dde6a750129): This model is used in the paper.
 * [GoogleNet](https://gist.github.com/jimmie33/339fd0a938ed026692267a60b44c0c58): This model is smaller, faster and slightly better than the VGG16 model.

It is recommended that you download the full system [here](https://github.com/jimmie33/SOD), which will automatically download all the needed models and data.

### Deep Hand: How to Train a CNN on 1 Million Hand Images When Your Data Is Continuous and Weakly Labelled

We provide pretrained CNN models of our CVPR'16 paper (Oral): 

    Deep Hand: How to Train a CNN on 1 Million Hand Images When Your Data Is Continuous and Weakly Labelled
    O. Koller, H. Ney, R. Bowden
    CVPR 2016, Las Vegas, NV, USA.
    
[[PDF](https://www-i6.informatik.rwth-aachen.de/publications/download/1000/KollerOscarNeyHermannBowdenRichard--DeepHHowtoTrainaCNNon1MillionHImagesWhenYourDataIsContinuousWeaklyLabelled--2016.pdf)] 
[[Webpage](http://www-i6.informatik.rwth-aachen.de/~koller/1miohands)]

### Mulimodal Compact Bilinear Pooling for VQA

The current state-of-the-art model for visual question answering, as described in the following paper:

```
@article{fukui16mcb,
  title={Multimodal Compact Bilinear Pooling for Visual Question Answering and Visual Grounding},
  author={Fukui, Akira and Park, Dong Huk and Yang, Daylen and Rohrbach, Anna and Darrell, Trevor and Rohrbach, Marcus},
  journal={arXiv:1606.01847},
  year={2016},
}
```

[[arXiv](https://arxiv.org/abs/1606.01847)] [[GitHub repo](https://github.com/akirafukui/vqa-mcb/)]

### Pose-Aware CNN Models (PAMs) for Face Recognition 

We provide the following:
- pretrained CNN models of our CVPR'16 paper for pose-aware face recognition in the wild
- [IJB-A](http://www.nist.gov/itl/iad/ig/facechallenges.cfm) yaw estimates from our pose estimation module 

_(your informations are required to proceed to the download page in the link below)_

``` latex
@INPROCEEDINGS{masi2016cvpr, 
    author={Iacopo Masi and Stephen Rawls and G{\'e}rard Medioni and Prem Natarajan}, 
    booktitle={CVPR}, 
    title={Pose-{A}ware {F}ace {R}ecognition in the {W}ild}, 
    year={2016}
    }
```
    
[[PDF](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Masi_Pose-Aware_Face_Recognition_CVPR_2016_paper.pdf)] 
[[Webpage](http://goo.gl/forms/NK6adyd7DFJhlmHG2)] 

### Learning Structured Sparsity in Deep Neural Networks

Train deep neural networks with structured sparsity to speed up DNNs:
```
@incollection{Wen_NIPS2016,
    Title = {Learning Structured Sparsity in Deep Neural Networks},
    Author = {Wen, Wei and Wu, Chunpeng and Wang, Yandan and Chen, Yiran and Li, Hai},
    bookTitle = {Advances in Neural Information Processing Systems},
    Year = {2016}
}
```

[[arXiv](http://arxiv.org/abs/1608.03665)] [[Caffemodel](https://drive.google.com/folderview?id=0B50edhjyQ0sRd3JLQ1V0OHdHcUE&usp=sharing)]  [[GitHub repo](https://github.com/wenwei202/caffe/tree/scnn)]


### Neural Activation Constellations: Unsupervised Part Model Discovery with Convolutional Networks

We provide fine-tuned  models for CUB200-2011 birds (AlexNet + VGG19), Oxford flowers 102 (AlexNet + VGG19), Oxford IIIT PETS (AlexNet + VGG19), and NABirds dataset (GoogLeNet). We also provide our AlexNet model which was trained on ImageNet with the Stanford dogs test data excluded. 

No bounding box or part annotations were used for fine-tuning. Part-based object proposal filtering and two-step fine-tuning was used as described in the corresponding paper

```
@inproceedings{Simon15:NAC,
    author = {Marcel Simon and Erik Rodner},
    booktitle = {International Conference on Computer Vision (ICCV)},
    title = {Neural Activation Constellations: Unsupervised Part Model Discovery with Convolutional Networks},
    year = {2015},
}
```

[[Models](https://drive.google.com/file/d/0B6VgjAr4t_oTQXN2Y3VYaEMwVDA/view?usp=sharing)] [[Paper](http://arxiv.org/abs/1504.08289)] [[Github repo](https://github.com/cvjena/part_constellation_models)] [[Slides](https://cms.rz.uni-jena.de/dbvmedia/de/Simon/ICCV15_SimonRodner_slides.pdf)]

### Inception-BN full ImageNet model
[![Try model on Haystack](https://img.shields.io/badge/try-on%20haystack-blue.svg)](https://www.haystack.ai/demos/Inception-Demo)

Inception-v2 model trained on full ImageNet dataset with 14,197,087 images in 21,841 classes. 

The model was converted from the MXNet InceptionBN-21k network trained by Mu Li. Details and evaluation results can be found at https://github.com/dmlc/mxnet-model-gallery/blob/master/imagenet-21k-inception.md.

```
@inproceedings{Ioffe15:ArXiv,
    author = {Sergey Ioffe and Christian Szegedy},
    booktitle = {arXiv:1502.03167},
    title = {Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift},
    year = {2015}
}
```

[[GitHub repo](https://github.com/pertusa/InceptionBN-21K-for-Caffe)] 
[[Paper](https://arxiv.org/abs/1502.03167)] 
[[Original MXNet network](https://github.com/dmlc/mxnet-model-gallery/blob/master/imagenet-21k-inception.md)]

### ResNet-101 for Face Recognition

This page contains a ResNet-101 deep network model, tuned for face recognition.

We fine-tuned this model using the procedure described in _I. Masi\*, A. Tran\*, T. Hassner\*, J. Leksut, G. Medioni, "Do We Really Need to Collect Million of Faces for Effective Face Recognition? "_, in Proc. of ECCV 2016 on the publicly available CASIA WebFace set.

_(your informations are required to proceed to the download page in the link below)_

Please, remember to cite our paper below, if you use our model, thanks.

``` latex
@inproceedings{masi16dowe,
      title={Do {W}e {R}eally {N}eed to {C}ollect {M}illions of {F}aces 
      for {E}ffective {F}ace {R}ecognition?},
      booktitle = {European Conference on Computer Vision},
      author={Iacopo Masi 
      and Anh Tran 
      and Tal Hassner 
      and Jatuporn Toy Leksut 
      and G\'{e}rard Medioni},
      year={2016},
    }
```
    
[[PDF](http://www.openu.ac.il/home/hassner/projects/augmented_faces/Masietal2016really.pdf)] 
[[Webpage](http://www.openu.ac.il/home/hassner/projects/augmented_faces/)] 

### DeepYeast

11-layer convolutional neural network trained on two-channel microscopy images of yeast cells carrying fluorescent proteins with different subcellular localizations.

[[Web](http://www.cs.ut.ee/~leopoldp/2016_DeepYeast)] 
[[Paper](http://biorxiv.org/content/early/2016/04/28/050757)] 
[[Model](http://www.cs.ut.ee/~leopoldp/2016_DeepYeast/code/caffe_model)]

### ImageNet pre-trained models with batch normalization
CNN models pre-trained on 1000 ImageNet categories. Currently contains:

* AlexNet and VGG16 with batch normalization added
* Residual Networks with 50 (ResNet-50) and 10 layers (ResNet-10)

Improves over previous pre-trained models and in particular reproduces the ImageNet results of ResNet50 using Caffe. Includes ResNet generation script, training code and log files.

```
@article{simon2016cnnmodels,
  Author = {Simon, Marcel and Rodner, Erik and Denzler, Joachim},
  Journal = {arXiv preprint arXiv:1612.01452},
  Title = {ImageNet pre-trained models with batch normalization},
  Year = {2016}
}
```

[[Models](https://github.com/cvjena/cnn-models)] [[Paper](https://arxiv.org/abs/1612.01452)] [[Website](http://www.inf-cv.uni-jena.de/Research/CNN+Models.html)]

### ResNet-101 for regressing 3D morphable face models (3DMM) from single images

This [project page](http://www.openu.ac.il/home/hassner/projects/CNN3DMM/)  contains a ResNet-101 deep network model for 3DMM regression (3D shape and texture)

The download includes both the network itself and the parameters required to map the 3DMM parameters regressed by the network back to 3D shapes
(e.g., the basis vectors for the face shape and the average face shape). 

If you find this useful, please remember to cite of paper below:

``` latex
@inproceedings{tran2017regressing,
  title={Regressing Robust and Discriminative 3D Morphable Models with a very Deep Neural Network},
  author={Tran, Anh Tuan and Hassner, Tal and Masi, Iacopo and Medioni, G\'{e}rard},
  booktitle={Computer Vision and Pattern Recognition (CVPR)},
  year={2017}
}
```
    
[[PDF](https://arxiv.org/abs/1612.04904)] 
[[Webpage](http://www.openu.ac.il/home/hassner/projects/CNN3DMM/)] 

### Cascaded Fully Convolutional Networks for Biomedical Image Segmentation
These models segment liver and liver tumor in CT volumes using the UNET architecture proposed by Ronnerberger et al. (2015). The [project](https://github.com/IBBM/Cascaded-FCN) contains all the source code, models and a notebook for easy liver and liver tumor inference. We encourage researcher to use our models for finetuning.

If you find this work useful for your research, please cite:
``` latex
@Inbook{Christ2016,
title="Automatic Liver and Lesion Segmentation in CT Using Cascaded Fully Convolutional Neural Networks and 3D Conditional Random Fields",
author="Christ, Patrick Ferdinand and Elshaer, Mohamed Ezzeldin A. and Ettlinger, Florian and Tatavarty, Sunil and Bickel, Marc and Bilic, Patrick and Rempfler, Markus and Armbruster, Marco and Hofmann, Felix and D'Anastasi, Melvin and Sommer, Wieland H. and Ahmadi, Seyed-Ahmad and Menze, Bjoern H.",
editor="Ourselin, Sebastien and Joskowicz, Leo and Sabuncu, Mert R. and Unal, Gozde and Wells, William",
bookTitle="Medical Image Computing and Computer-Assisted Intervention -- MICCAI 2016: 19th International Conference, Athens, Greece, October 17-21, 2016, Proceedings, Part II",
year="2016",
publisher="Springer International Publishing",
address="Cham",
pages="415--423",
isbn="978-3-319-46723-8",
doi="10.1007/978-3-319-46723-8_48",
url="http://dx.doi.org/10.1007/978-3-319-46723-8_48"
}
```
[[PDF](https://arxiv.org/abs/1610.02177)] 
[[Webpage](https://github.com/IBBM/Cascaded-FCN)]
[[Models](https://github.com/IBBM/Cascaded-FCN)]  

### Deep Networks for Earth Observation
These models have been trained to perform semantic segmentation on aerial images, as proposed by Audebert et al. (2016). The available models are based on the SegNet architecture (Kendall et al., 2015). The [project repository](https://github.com/nshaud/DeepNetsForEO) contains the model definitions and pre-trained weights on the city of Vaihingen.

```latex
@inproceedings{audebert_semantic_2016,
    address = {Taipei, Taiwan},
    title = {Semantic {Segmentation} of {Earth} {Observation} {Data} {Using} {Multimodal} and {Multi}-scale {Deep} {Networks}},
    url = {https://hal.archives-ouvertes.fr/hal-01360166},
    urldate = {2016-10-13},
    booktitle = {Asian {Conference} on {Computer} {Vision} ({ACCV}16)},
    author = {Audebert, Nicolas and Le Saux, Bertrand and Lefèvre, Sébastien},
    month = nov,
    year = {2016},
    keywords = {computer vision, data fusion, Earth observation, Neural networks, remote sensing},
}
```
[[PDF](https://arxiv.org/abs/1609.06846)] 
[[Project](https://github.com/nshaud/DeepNetsForEO)] 

### Supervised Learning of Semantics-Preserving Hash via Deep Convolutional Neural Networks
We present a simple yet effective supervised deep hash approach that constructs binary hash codes from labeled data for large-scale image search. The supervised semantics-preserving deep hashing (SSDH) constructs hash functions as a latent layer in a deep network and the binary codes are learned by minimizing an objective function defined over classification error and other desirable hash codes properties. This is the extended version of our "[CVPRW'15 paper.](http://www.iis.sinica.edu.tw/~kevinlin311.tw/cvprw15.pdf)" The details can be found in the following "[TPAMI'17 paper](https://arxiv.org/pdf/1507.00101v2.pdf)":

    Supervised Learning of Semantics-Preserving Hash via Deep Convolutional Neural Networks
    Huei-Fang Yang, Kevin Lin, Chu-Song Chen
    IEEE Transactions on Pattern Analysis and Machine Intelligence (​TPAMI), 2017

please cite the paper if you use the model:
 * [Caffe-DeepBinaryCode](https://github.com/kevinlin311tw/Caffe-DeepBinaryCode): See our code release on Github, which allows you to train your own deep hashing model and create binary hash codes.

### Striving for Simplicity: The All Convolutional Net

Implementation of All-CNN-C model for CIFAR-10 from the paper _Striving for Simplicity: The All Convolutional Net_ by Jost Tobias Springenberg, Alexey Dosovitskiy, Thomas Brox, Martin Riedmiller, accepted as a workshop contribution at ICLR 2015.

``` latex
@article{Springenberg14,
  author    = {Jost Tobias Springenberg and Alexey Dosovitskiy and Thomas Brox and Martin A. Riedmiller},
  title     = {Striving for Simplicity: The All Convolutional Net},
  year      = {2014},
}
```
[[arXiv](https://arxiv.org/abs/1412.6806)] [[GitHub repo](https://github.com/mateuszbuda/ALL-CNN)]