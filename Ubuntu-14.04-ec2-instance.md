Welcome to Pete Warden's guide to setting up Caffe in an ec2 instance with Ubuntu 14.04.

[https://vimeo.com/101582001](https://vimeo.com/101582001)

There's a Vagrant VM created with these steps at `https://d2rlgkokhpr1uq.cloudfront.net/dl_webcast.box`

An Amazon EC2 AMI is available for the Northern California zone as `ami-2faaa96a`

Below are the steps I followed to create that image.

Start with `ami-a7fdfee2` in Northern California, Ubuntu Server 14.04

Choose an m3.medium instance

SSH into the instance

```shell
sudo apt-get install linux-headers-`uname -r`
curl -O "http://developer.download.nvidia.com/compute/cuda/6_5/rel/installers/cuda_6.5.14_linux_64.run"

sudo apt-get update
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gcc-4.6 g++-4.6 gcc-4.6-multilib g++-4.6-multilib gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip

sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc-4.6 30
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++-4.6 30
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 30
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 30

chmod +x cuda_6.5.14_linux_64.run
sudo ./cuda_6.5.14_linux_64.run --kernel-source-path=/usr/src/linux-headers-`uname -r`/
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

After 'make all', you may face two errors. Here are the solutions: 

Error One: 
```shell
./include/caffe/common.hpp:5:27: fatal error: gflags/gflags.h: No such file or directory
compilation terminated.
```
Solutions: 
```shell
wget https://github.com/schuhschuh/gflags/archive/master.zip
unzip master.zip
cd gflags-master
mkdir build && cd build
export CXXFLAGS="-fPIC" && cmake .. && make VERBOSE=1
make 
sudo make install
```

Error Two: 
```shell
./include/caffe/data_layers.hpp:11:18: fatal error: lmdb.h: No such file or directory
```

Solution: 
```shell
git clone git://gitorious.org/mdb/mdb.git
cd mdb/libraries/liblmdb
make
sudo make install
```
After the installation of caffe, you could build the python interfance for it:

```shell
sudo ln -s /usr/include/python2.7/ /usr/local/include/python2.7
sudo ln -s /usr/local/lib/python2.7/dist-packages/numpy-1.8.1-py2.7-linux-x86_64.egg/numpy/core/include/numpy /usr/local/include/python2.7/numpy
make pycaffe
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/lib' >> ~/.bashrc
source ~/.bashrc
sudo easy_install pillow
```

If when you run 'make pycaffe', you see this error
```shell
UnicodeDecodeError: 'ascii' codec can't decode byte 0xe2 in position 54: ordinal not in range(128)
```

you could fix it by running: 
```shell
sudo apt-get install libevent-dev python-dev
```
That should be the end of the installation. You can test that it runs with:
```shell
python python/classify.py --print_results examples/images/cat.jpg foo
```

The expected output is:
```shell
[('kit fox', '0.27327'), ('red fox', '0.20591'), ('wood rabbit', '0.12281'), ('Egyptian cat', '0.06716'), ('hare', '0.06573')]
```