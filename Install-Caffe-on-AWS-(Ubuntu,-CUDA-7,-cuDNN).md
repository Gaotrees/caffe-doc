# Install Caffe on AWS from scratch

### Overview

By the end of this tutorial, you will have successfully installed CUDA 7 and cuDNNv2 working with Caffe on AWS using a g2.2xlarge or g2.8xlarge instance using Ubuntu 14.04.

This guide was tested in May 2015.

Keywords: AWS, GPU, amazon, caffe, install, how, to

### Begin Tutorial

This guide also applies to standard desktop Ubuntu installations.

Start up one of Amazon GPU instances (g2.2xlarge or g2.8xlarge) using Ubuntu 64 bit (HVM) and **NOT** Amazon's AMI. Make sure to attach both instance store 0 and instance store 1 in the "Add Storage" step. Also increase the Root `/dev/sda1` device size to something larger than 8 GiB.

#### Installing the NVIDIA Drivers
Update and install the preliminaries:
```Shell
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install build-essential
```

Note: Amazon says you must use the 340.46 driver ([see the official GPU documentation here](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using_cluster_computing.html)) but this guide works while using the most recent NVIDIA driver 346.46.

Download the "run" CUDA installer (which includes the NVIDIA driver) from NVIDIA's website. The link is [usually here](https://developer.nvidia.com/cuda-downloads).
```
wget http://developer.download.nvidia.com/compute/cuda/7_0/Prod/local_installers/cuda_7.0.28_linux.run
```

Extract all the installers:
```Shell
chmod +x cuda_7.0.28_linux.run
mkdir nvidia_installers
./cuda_7.0.28_linux.run -extract=`pwd`/nvidia_installers
```

Then update the linux image to be compatible with NVIDIA's drivers:
```
sudo apt-get install linux-image-extra-virtual
```
**Important:** While installing the linux-image-extra-virtual, you may be prompted "*What would you like to do about menu.lst?*" I selected "**keep the local version currently installed**"

We now need to disable nouveau since it conflicts with NVIDIA's kernel module:
```Shell
sudo vi /etc/modprobe.d/blacklist-nouveau.conf
```

And add the following lines to this file:
```Shell

blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
Back in the terminal/shell, execute the commands:
```Shell
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
sudo update-initramfs -u
sudo reboot
```

After the reboot is complete, we have a few more steps:
```Shell
sudo apt-get install linux-source
sudo apt-get install linux-headers-`uname -r`
```
Now we can finally install the driver:
```Shell
cd nvidia_installers
sudo ./NVIDIA-Linux-x86_64-346.46.run
```
1. Accept the license agreement.
2. If you see: "nvidia-installer was forced to guess the X library path '/usr/lib' and X module path ..." go ahead anc click OK.
3. If you see "The CC version check failed" then click "Ignore CC version check".
4. It may ask you about 32-bit libraries, I selected to yes, install them.
5. It will ask you about running nvidia-xconfig to update your X configuration file. I selected no.
6. Run `nvidia-smi` to view the installed GPUs.

#### Installing CUDA
Now we can install CUDA and optionally the examples. Make sure to run `sudo modprobe nvidia` first.
```Shell
sudo modprobe nvidia
sudo apt-get install build-essential
sudo ./cuda-linux64-rel-7.0.28-19326674.run
sudo ./cuda-samples-linux-7.0.28-19326674.run
```
1. Sometimes it is not necessary to reinstall `build-essential`.
2. When the license agreement appears, press "q" so you don't have to scroll down.
3. Accept the EULA.
4. Use the default path by pressing enter.
5. *Would you like to add desktop menu shortcuts?* Answer depends on your preference.
6. *Would you like to create a symbolic link?* Enter yes.
7. It will now install CUDA.

Finally, update your path variables. Open your `~/.bashrc` file and ad the following lines:
```Shell
export PATH=$PATH:/usr/local/cuda-7.0/bin
export LD_LIBRARY_PATH=:/usr/local/cuda-7.0/lib64
```
Remember to run `source ~/.bashrc` after saving `.bashrc`

#### Installing cuDNN
After registering with NVIDA, download cuDNN. Extract the tar and copy the headers and libraries to the CUDA directory.
```Shell
wget http://albert.cm/dl/cudnn-6.5-linux-x64-v2.tgz
tar -zxf cudnn-6.5-linux-x64-v2.tgz
cd cudnn-6.5-linux-x64-v2
sudo cp lib* /usr/local/cuda/lib64/
sudo cp cudnn.h /usr/local/cuda/include/
```

#### Installing Caffe
Install the dependencies:
```Shell
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip libgoogle-glog-dev libbz2-dev libxml2-dev libxslt-dev libffi-dev libssl-dev libgflags-dev liblmdb-dev python-yaml python-numpy
```
Then run:
```Shell
sudo easy_install pillow
```
Now we can download Caffe. Navigate to the directory of your choice for the cloning.
```Shell
cd ~
git clone https://github.com/BVLC/caffe.git
```
We now install more dependencies. **Warning: This takes 10-30 minutes.**
```Shell
cd caffe
cat python/requirements.txt | xargs -L 1 sudo pip install
```

Now we update the Makefile:
```Shell
cp Makefile.config.example Makefile.config
vi Makefile.config
```

1. Uncomment the line: `USE_CUDNN := 1`
2. Make sure the `CUDA_DIR` correctly points to our CUDA installation.
3. If you want the Matlab wrapper, uncomment the appropriate `MATLAB_DIR` line.

Now we build Caffe. **Set X to the number of CPU threads (or cores) on your machine.** Use the command `htop` to check how many CPU threads you have.
```Shell
make pycaffe -jX
make all -jX
make test -jX
```

Now to quickly test Caffe, from the `CAFFE_ROOT` (wherever the Caffe code resides)
```Shell
./data/mnist/get_mnist.sh
./examples/mnist/create_mnist.sh
./examples/mnist/train_lenet.sh
```
You may get errors for `create_mnist.sh` but run `train_lenet.sh` anyway. Chances are it will still work. If you see the network training, then everything has been successfully set up. 
