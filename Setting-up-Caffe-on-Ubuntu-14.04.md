The original version of this tutorial - written by Pete Warden - uses CUDA 6.0 and comes with a one hour video walk-through and a pre-configured Vagrant VM. Since Pete wrote his tutorial, CUDA 6.5 has been released and a couple of the involved steps have become simpler. If you want to set up your own system from scratch, you should probably go for the tutorial based on CUDA 6.5. If, on the other hand, you want less hassle and just want to try out a working system, you are probably better off with the original CUDA 6.0 based tutorial.

## Using CUDA 6.5
* Download newest Ubuntu release. I used KUbuntu from http://cdimage.ubuntu.com/kubuntu/releases/trusty/release/kubuntu-14.04.1-desktop-amd64.iso
* Start VirtualBox, create a new virtual machine (Linux/Ubuntu/64bit/DynamicHD/8GbRAM/…). Then start the VM from the downloaded .iso (do this from inside VirtualBox). Installation of Kubuntu will begin.
* Install system updates (3.13.0-32 -> 3.13.0-36)
* Install VBox Additions:
  * Click the USB icon in the task-bar (lower right of screen)
  * Left click the VBOXADDITIONS_4.3.16_95972
  * Select “Open with File Manager” (this will mount the virtual CD in the virtual CD drive…). Once the file manager window has opened, you can kill it. This step is only needed to mount the CD...
  * `cd /media/<USER>/VBOXADDITIONS_4.3.16_95972` (where `<USER>` is your user name)
  * `sudo ./VBoxLinuxAdditions.run`
* Activate bidirectional clip-board:
  * In Virtual Box Manager, click Settings, then General | Advanced | Shared Clipboard
* Install build essentials:
  * `sudo apt-get install build-essential`
* Install latest version of kernel headers:
  * ``sudo apt-get install linux-headers-`uname -r` ``
* Install curl (for the CUDA download):
  * `sudo apt-get install curl`
* Download CUDA.
  * `cd ~/Downloads/`
  * `curl -O "http://developer.download.nvidia.com/compute/cuda/6_5/rel/installers/cuda_6.5.14_linux_64.run"`
* Make the downloaded installer file runnable:
  * `chmod +x cuda_6.5.14_linux_64.run`
* Run the CUDA installer:
  * ``sudo ./cuda_6.5.14_linux_64.run --kernel-source-path=/usr/src/linux-headers-`uname -r`/ ``
    * Accept the EULA
    * Do **NOT** install the graphics card drivers (since we are in a virtual machine)
    * Install the toolkit (leave path at default)
    * Install symbolic link
    * Install samples (leave path at default)
* Update the library path
  * `echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/lib' >> ~/.bashrc`
  * `source ~/.bashrc`
* Install dependencies:
  * `sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip libgoogle-glog-dev libbz2-dev libxml2-dev libxslt-dev libffi-dev libssl-dev libgflags-dev liblmdb-dev python-yaml`
  * `sudo easy_install pillow`
* Download Caffe:
  * `git clone https://github.com/BVLC/caffe.git`
* The standard installation of dependencies for Caffe **FAILS** (so don't do this):
  * `sudo pip install -r python/requirements.txt` (**FAILS**)
    * `Command python setup.py egg_info failed with error code 1 in /tmp/pip_build_root/scikit-image`
* Instead run `sudo pip install` on each of the entries of `python/requirements.txt`. This works for all except one, which can be installed with `easy_install` instead:
  * `sudo pip install Cython`
  * `sudo pip install h5py`
  * `sudo pip install ipython`
  * `sudo pip install leveldb`
  * `sudo pip install matplotlib`
  * `sudo pip install networkx`
  * `sudo pip install nose` (already installed by something else)
  * `sudo pip install numpy` (already installed by something else)
  * `sudo pip install pandas`
  * `sudo pip install protobuf` (**FAILS**)
    * `pkg_resources.VersionConflict: (python-dateutil 2.2 (/usr/local/lib/python2.7/dist-packages), Requirement.parse('python-dateutil>=1.4,<2'))
  * `sudo easy_install protobuf` (This works)
  * `sudo pip install python-gflags`
  * `sudo pip install scikit-image`
  * `sudo pip install scikit-learn`
  * `sudo pip install scipy`
* Add a couple of symbolic links for some reason:
  * `sudo ln -s /usr/include/python2.7/ /usr/local/include/python2.7`
  * `sudo ln -s /usr/local/lib/python2.7/dist-packages/numpy/core/include/numpy/ /usr/local/include/python2.7/numpy`
* Compile Caffe:
  * `make pycaffe`
  * `make all`
  * `make test`
* Download the ImageNet Caffe model and labels:
  * `./scripts/download_model_binary.py models/bvlc_reference_caffenet`
  * `./data/ilsvrc12/get_ilsvrc_aux.sh`
* Modify `python/classify.py` to add the `--print_results` option
  * Compare `https://github.com/jetpacapp/caffe/blob/master/python/classify.py` (version from 2014-07-18) to the current version of `classify.py` in the official Caffe distribution `https://github.com/BVLC/caffe/blob/master/python/classify.py` 
* Test your installation by running the ImageNet model on an image of a kitten:
  * `cd ~/caffe` (or whatever you called your Caffe directory)
  * `python python/classify.py --print_results examples/images/cat.jpg foo`
  * Expected result: `[('tabby', '0.27933'), ('tiger cat', '0.21915'), ('Egyptian cat', '0.16064'), ('lynx', '0.12844'), ('kit fox', '0.05155')]`
* Test your installation by training a net on the MNIST dataset of handwritten digits:
  * `cd ~/caffe` (or whatever you called your Caffe directory)
  * `./data/mnist/get_mnist.sh`
  * `./examples/mnist/create_mnist.sh`
  * `./examples/mnist/train_lenet.sh`
  * See http://caffe.berkeleyvision.org/gathered/examples/mnist.html for more information...

## Using CUDA 6.0
I've created a video documenting the setup steps I used on Ubuntu 14.04 here:

[https://vimeo.com/101582001](https://vimeo.com/101582001)

There's a Vagrant VM created with these steps at `https://d2rlgkokhpr1uq.cloudfront.net/dl_webcast.box`

An Amazon EC2 AMI is available for the Northern California zone as `ami-2faaa96a`

Below are the steps I followed to create that image.

Start with `ami-a7fdfee2` in Northern California, Ubuntu Server 14.04

Choose an m3.medium instance

SSH into the instance

```shell
sudo apt-get install linux-headers-`uname -r`
curl -O "http://developer.download.nvidia.com/compute/cuda/6_0/rel/installers/cuda_6.0.37_linux_64.run"

sudo apt-get update
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gcc-4.6 g++-4.6 gcc-4.6-multilib g++-4.6-multilib gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip

sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc-4.6 30
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++-4.6 30
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 30
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 30

chmod +x cuda_6.0.37_linux_64.run
sudo ./cuda_6.0.37_linux_64.run --kernel-source-path=/usr/src/linux-headers-`uname -r`/
```
Press 'q' on the EULA, 'accept', 'y', 'n' on driver, 'y' on toolkit, return on location, 'y' on symlink, 'n' on samples.

```shell
wget https://google-glog.googlecode.com/files/glog-0.3.3.tar.gz
tar zxvf glog-0.3.3.tar.gz
cd glog-0.3.3
./configure
make
sudo make install
cd ..

git clone https://github.com/jetpacapp/caffe.git
```
Replace this with https://github.com/BVLC/caffe.git for the official fork.

```shell
cd caffe
cp Makefile.config.example Makefile.config
echo "CXX := /usr/bin/g++-4.6" >> Makefile.config
sed -i 's/CXX :=/CXX ?=/' Makefile
make all
make test
examples/imagenet/get_caffe_reference_imagenet_model.sh
mv caffe_reference_imagenet_model examples/imagenet
data/ilsvrc12/get_ilsvrc_aux.sh

sudo pip install -r python/requirements.txt
sudo easy_install numpy
sudo pip install -r python/requirements.txt
```

I had to run the requirements twice because there seems to be a scikit-image dependency on numpy, so the first run failed.

```shell
sudo ln -s /usr/include/python2.7/ /usr/local/include/python2.7
sudo ln -s /usr/local/lib/python2.7/dist-packages/numpy-1.8.1-py2.7-linux-x86_64.egg/numpy/core/include/numpy /usr/local/include/python2.7/numpy
make pycaffe
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/lib' >> ~/.bashrc
source ~/.bashrc
sudo easy_install pillow
```

That should be the end of the installation. You can test that it runs with:
```shell
python python/classify.py --print_results examples/images/cat.jpg foo
```

The expected output is:
```shell
[('kit fox', '0.27327'), ('red fox', '0.20591'), ('wood rabbit', '0.12281'), ('Egyptian cat', '0.06716'), ('hare', '0.06573')]
```