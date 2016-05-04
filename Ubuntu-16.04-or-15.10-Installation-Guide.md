The following guide includes the how-to instructions for the installation of BVLC/Caffe in Ubuntu 16.04 or 15.10 Linux. This also includes the KUbuntu 16.04 or 15.10 and the related distributions.

Execute these commands first:

```shell

sudo apt-get update

sudo apt-get upgrade

sudo apt-get install build-essential cmake git pkg-config

sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler

sudo apt-get install --no-install-recommends libboost-all-dev

sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

(Python 2.7 development files)
sudo apt-get install python-dev

(or, Python 3.5 development files)
sudo apt-get install python3-dev

(OpenCV 2.4)
sudo apt-get install libopencv-dev

(or, OpenCV 3.1 - see the instructions below)

```

For the instructions on how to use the OpenCV version 3.1, please see https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-OpenCV-3.1-Installation-Guide

The configuration settings will differ for OpenCV 3.1 as you can see above, but here we continue with the basic settings that imply the version 2.x.

Go to the https://github.com/BVLC/caffe and download zip archive. Unpack it to ~/bin/ or any other location. Enter the caffe-master directory in the terminal window.

Copy the Makefile.config.example to Makefile.config like this:

```
cp Makefile.config.example Makefile.config
```

and open it for editing (with a text editor). I use the kate editor for this purpose, so the command that I execute goes as follows. You first need to install the kate editor with:

```
sudo apt-get install kate
```

and then you can edit the configuration file with:

```
kate ./Makefile.config &
```

The following line in the configuration file tells the program to use CPU only for the computations. 

> CPU_ONLY := 1

This is the typical setting for a computer without any NVIDIA graphics card and it is typical for the installation of Caffe inside the typical virtual machine. (Notice that there is a special type of virtual machine inside the Ubuntu host machine that can access the physical NVIDIA graphics card directly. See https://github.com/NVIDIA/nvidia-docker)

Change the line accordingly by commenting it out (# CPU_ONLY := 1) if you have an NVIDIA graphics card with the proprietary driver, CUDA toolkit and CUDNN installed. The Makefile.config should contain the following lines, so find them and fill them in.

> PYTHON_INCLUDE := /usr/include/python2.7 /usr/lib/python2.7/dist-packages/numpy/core/include  

> (For ways to create an isolated Python environment, explore the topic of virtual environments here: http://docs.python-guide.org/en/latest/dev/virtualenvs/)

> WITH_PYTHON_LAYER := 1

> INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include /usr/include/hdf5/serial

> LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial


Now lets continue with the instructions for version 15.10.

Execute the additional commands:

```
find . -type f -exec sed -i -e 's^"hdf5.h"^"hdf5/serial/hdf5.h"^g' -e 's^"hdf5_hl.h"^"hdf5/serial/hdf5_hl.h"^g' '{}' \;

cd /usr/lib/x86_64-linux-gnu

sudo ln -s libhdf5_serial.so.8.0.2 libhdf5.so

sudo ln -s libhdf5_serial_hl.so.8.0.2 libhdf5_hl.so
```

In Ubuntu 16.04, the file versions are different. Visit /usr/lib/x86_64-linux-gnu/ and list the contents. Thee versions are 10.1.0 and 10.0.2 respectively.

Now lets return to the unpacked Caffe directory caffe-master and enter these commands:

```
cd python

for req in $(cat requirements.txt); do pip install $req; done
```


--------------------------------------------------------------------------------------------------------------


NOTE: If the Ubuntu operating system was updated, perhaps the Python layer needs to be updated and recompiled, because the Python module no longer works. Perform this step again in that case.

```
for req in $(cat requirements.txt); do pip install $req; done

In case of any problems, try:

for req in $(cat requirements.txt); do sudo -H pip install $req --upgrade; done
```


--------------------------------------------------------------------------------------------------------------


Next, execute:

```
cd ..

(now you are in caffe-master directory)

make all

make test

make runtest

make pycaffe      -should be finished already, so you can omit this one

make distribute
```

In order to make the Python work with Caffe, open the file ~/.bashrc for editing in your favorite text editor. There, add the following line at the end of file:

> export PYTHONPATH=/path/to/caffe-master/python:$PYTHONPATH

You can also execute that same line immediately as a command for immediate effects.

In order to use the Caffe binaries, libraries, or include files, they need to be reachable through the search path, so one solution is to copy them into their respective directories: from the distribute directory to the /usr/bin or /usr/lib or /usr/include.

* Models download not covered in these instructions. See https://github.com/BVLC/caffe/wiki/Model-Zoo *


For most Linux programs compiled from source, you can attempt to build a package that can be installed and uninstalled with a single click.

```
sudo apt-get install checkinstall
```

Now, when you execute the:

```
sudo checkinstall
```

and fill out a form with some easy questions, you will have the package made automatically. However, this uses the command "make install" in the background, which will fail, because the Caffe project does not have the target "install" configured in the Makefile.

----------------------------------------------------------------------------------------------------

### The GPU support prerequisites


In Ubuntu 15.10, enable the use of proprietary drivers in the Software & Updates Center for your desktop and install the NVIDIA graphics driver first from the main Ubuntu package repository. See https://help.ubuntu.com/community/BinaryDriverHowto/Nvidia

Download the CUDA toolkit network installer and the CUDNN package from the NVIDIA site, after registering and filling out the forms.
https://developer.nvidia.com/cuda-downloads

Install the cuda toolkit 7.5 version manually in the terminal as instructed
at the website.

```
sudo dpkg -i cuda-repo-ubuntu1504_7.5-18_amd64.deb

sudo apt-get update

sudo apt-get install cuda
```


Download and unpack as root user CUDNN from https://developer.nvidia.com/cudnn.

Put all CUDNN files manually starting with the search path directory where the CUDA toolkit is, each file in its own respective directory. That directory could be /usr/local/cuda.

You can check your Ubuntu environment variables after the reboot, by executing the command:

```
export
```

Edit the Makefile.config in Caffe directory accordingly (as described in the config file itself) and recompile the Caffe to support the GPU computation. To recompile, first execute "make clean".

----------------------------------------------------------------------------------------