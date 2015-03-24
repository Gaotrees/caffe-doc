Trained models are posted here as links to Github Gists.
Check out the [model zoo documentation](http://caffe.berkeleyvision.org/model_zoo.html) for details.

To acquire a model:

1. download the model gist by `./scripts/download_model_from_gist.sh <gist_id> <dirname>` to load the model metadata, architecture, solver configuration, and so on. (`<dirname>` is optional and defaults to caffe/models).
2. download the model weights by `./scripts/download_model_binary.py <model_dir>` where `<model_dir>` is the gist directory from the first step.

### Berkeley-trained models

 - [Finetuning on Flickr Style](https://gist.github.com/sergeyk/034c6ac3865563b69e60): same as provided in `models/`, but listed here as a Gist for an example.
 - [BVLC GoogleNet](https://gist.github.com/sguada/866e2aa1fd707b89b913)

### Network in Network model
The Network in Network model is described in the following [ICLR-2014 paper](http://arxiv.org/abs/1312.4400):

    Network In Network
    M. Lin, Q. Chen, S. Yan
    International Conference on Learning Representations, 2014 (arXiv:1409.1556)

please cite the paper if you use the models.

Models:
 * [NIN-Imagenet](https://gist.github.com/mavenlin/d802a5849de39225bcc6): a small(29MB) model for imagenet, yet performs slightly better than AlexNet, and fast to train.
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

The project page is at [here](http://places.csail.mit.edu)

Models:
 * [Places205-CNN](http://places.csail.mit.edu/model/placesCNN.tar.gz): CNN trained on 205 scene categories of Places Database (used in NIPS'14) with ~2.5 million images. The architecture is the same as Caffe reference network.
 * [Hybrid-CNN](http://places.csail.mit.edu/model/hybridCNN.tar.gz): CNN trained on 1183 categories (205 scene categories from Places Database and 978 object categories from the train data of ILSVRC2012 (ImageNet) with ~3.6 million images. The architecture is the same as Caffe reference network.

### GoogLeNet GPU implementation from Princeton.
We implemented GoogLeNet using a single GPU. Our main contribution is an effective way to initialize the network and a trick to overcome the GPU memory constrain by accumulating gradients over two training iterations. 
* Please check [http://vision.princeton.edu/pvt/GoogLeNet/](http://vision.princeton.edu/pvt/GoogLeNet/) for more information. Pre-trained models on ImageNet and Places, and the training code are available for download.
* Make sure cls2_fc2 and cls3_fc have num_output = 1000 in the prototxt. Otherwise, the trained model would crash on test.

### <a name="fcn"></a>Fully Convolutional Semantic Segmentation Models (FCN-Xs)

These models are described in the [paper](http://cs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf):

    Fully Convolutional Models for Semantic Segmentation
    Jonathan Long, Evan Shelhamer, Trevor Darrell
    arXiv:1411.4038

These are pre-release models. They do not run in any current version of BVLC/caffe, as they require unmerged PRs. They should run in the preview branch provided at https://github.com/longjon/caffe/tree/future.

Models trained on PASCAL (using extra data from [Hariharan et al.](http://www.cs.berkeley.edu/~bharath2/codes/SBD/download.html) and finetuned from the ILSVRC-trained VGG-16 model above):
* [FCN-32s PASCAL](https://gist.github.com/longjon/ac410cad48a088710872#file-readme-md): single stream, 32 pixel prediction stride version
* [FCN-16s PASCAL](https://gist.github.com/longjon/d24098e083bec05e456e#file-readme-md): two stream, 16 pixel prediction stride version
* [FCN-8s PASCAL](https://gist.github.com/longjon/1bf3aa1e0b8e788d7e1d#file-readme-md): three stream, 8 pixel prediction stride version

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
https://gist.github.com/jgoode21/0179e52305ca768a601f

The is the reference CaffeNet (modified [AlexNet](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)) fine-tuned for the [Oxford 102 category flower dataset](http://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html). The number of outputs in the inner product layer has been set to 102 to reflect the number of flower categories. Hyperparameter choices reflect those in [Fine-tuning CaffeNet for Style Recognition on “Flickr Style” Data](http://caffe.berkeleyvision.org/gathered/examples/finetune_flickr_style.html). The global learning rate is reduced while the learning rate for the final fully connected is increased relative to the other layers.

After 50,000 iterations, the top-1 error is 7% on the test set of 1,020 images.

```
I0215 15:28:06.417726  6585 solver.cpp:246] Iteration 50000, loss = 0.000120038
I0215 15:28:06.417789  6585 solver.cpp:264] Iteration 50000, Testing net (#0)
I0215 15:28:30.834987  6585 solver.cpp:315]     Test net output #0: accuracy = 0.9326
I0215 15:28:30.835072  6585 solver.cpp:251] Optimization Done.
I0215 15:28:30.835083  6585 caffe.cpp:121] Optimization Done.
```