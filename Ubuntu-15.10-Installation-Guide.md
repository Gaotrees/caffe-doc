The following guide includes the how-to instructions for the installation of BVLC/Caffe in Ubuntu 15.10 Linux. This also includes the KUbuntu 15.10 and the related distributions.

sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake git pkg-config
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install python-dev


Go to the https://github.com/BVLC/caffee and download zip archive. Unpack it to ~/bin/ or any other location. Enter the directory in the terminal window.

Copy the Makefile.config.example to Makefile.config like this:
cp Makefile.config.example Makefile.config
and open it for editing (with a text editor).

The following example uses CPU only for the computations. Change it accordingly if you have an NVIDIA graphics card with the proprietary driver, CUDA toolkit and CUDNN installed on a real, physical machine. 


''###################################################################'
'## Refer to http://caffe.berkeleyvision.org/installation.html'
'# Contributions simplifying and improving our build system are welcome!'
''
'# cuDNN acceleration switch (uncomment to build with cuDNN).'
'# USE_CUDNN := 1'
''
'# CPU-only switch (uncomment to build without GPU support).'
'CPU_ONLY := 1'
''
'# uncomment to disable IO dependencies and corresponding data layers'
'# USE_OPENCV := 0'
'# USE_LEVELDB := 0'
'# USE_LMDB := 0'
''
'# uncomment to allow MDB_NOLOCK when reading LMDB files (only if necessary)''
'# You should not set this flag if you will be reading LMDBs with any'
'# possibility of simultaneous read and write'
'# ALLOW_LMDB_NOLOCK := 1'
''
'# Uncomment if you're using OpenCV 3'
'# OPENCV_VERSION := 3'
''
'# To customize your choice of compiler, uncomment and set the following.'
'# N.B. the default for Linux is g++ and the default for OSX is clang++'
'# CUSTOM_CXX := g++'
''
'# CUDA directory contains bin/ and lib/ directories that we need.'
'CUDA_DIR := /usr/local/cuda'
'# On Ubuntu 14.04, if cuda tools are installed via'
'# "sudo apt-get install nvidia-cuda-toolkit" then use this instead:'
'# CUDA_DIR := /usr'
''
'# CUDA architecture setting: going with all of them.'
'# For CUDA < 6.0, comment the *_50 lines for compatibility.'
'CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \'
'-gencode arch=compute_20,code=sm_21 \'
'-gencode arch=compute_30,code=sm_30 \'
'-gencode arch=compute_35,code=sm_35 \'
'-gencode arch=compute_50,code=sm_50 \'
'-gencode arch=compute_50,code=compute_50'
''
'# BLAS choice:'
'# atlas for ATLAS (default)''
'# mkl for MKL'
'# open for OpenBlas'
'BLAS := atlas'
'# Custom (MKL/ATLAS/OpenBLAS) include and lib directories.'
'# Leave commented to accept the defaults for your choice of BLAS'
'# (which should work)!'
'# BLAS_INCLUDE := /path/to/your/blas'
'# BLAS_LIB := /path/to/your/blas'
''
'# Homebrew puts openblas in a directory that is not on the standard search path'
'# BLAS_INCLUDE := $(shell brew --prefix openblas)/include'
'# BLAS_LIB := $(shell brew --prefix openblas)/lib'
''
'# This is required only if you will compile the matlab interface.'
'# MATLAB directory should contain the mex binary in /bin.'
'# MATLAB_DIR := /usr/local'
'# MATLAB_DIR := /Applications/MATLAB_R2012b.app'
''
'# NOTE: this is required only if you will compile the python interface.'
'# We need to be able to find Python.h and numpy/arrayobject.h.'
'PYTHON_INCLUDE := /usr/include/python2.7 \'
'/usr/lib/python2.7/dist-packages/numpy/core/include'
'# Anaconda Python distribution is quite popular. Include path:'
'# Verify anaconda location, sometimes it's in root.'
'# ANACONDA_HOME := $(HOME)/anaconda'
'# PYTHON_INCLUDE := $(ANACONDA_HOME)/include \'
'# $(ANACONDA_HOME)/include/python2.7 \'
''# $(ANACONDA_HOME)/lib/python2.7/site-packages/numpy/core/include \'
''
'# We need to be able to find libpythonX.X.so or .dylib.'
'PYTHON_LIB := /usr/lib'
'# PYTHON_LIB := $(ANACONDA_HOME)/lib'
''
'# Homebrew installs numpy in a non standard path (keg only)''
'# PYTHON_INCLUDE += $(dir $(shell python -c 'import numpy.core;'
'print(numpy.core.__file__)'))/include'
'# PYTHON_LIB += $(shell brew --prefix numpy)/lib'
''
'# Uncomment to support layers written in Python (will link against Python libs)''
'WITH_PYTHON_LAYER := 1'
''
'# Whatever else you find you need goes here.'
'INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include'
'/usr/include/hdf5/serial'
'LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib'
'/usr/lib/x86_64-linux-gnu/hdf5/serial'
''
'# If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies'
'# INCLUDE_DIRS += $(shell brew --prefix)/include'
'# LIBRARY_DIRS += $(shell brew --prefix)/lib'
''
'# Uncomment to use `pkg-config` to specify OpenCV library paths.'
'# (Usually not necessary -- OpenCV libraries are normally installed in one of the above $LIBRARY_DIRS.)'
'# USE_PKG_CONFIG := 1'
''
'BUILD_DIR := build'
'DISTRIBUTE_DIR := distribute'
''
'# Uncomment for debugging. Does not work on OSX due to https://github.com/BVLC/caffe/issues/171'
'# DEBUG := 1'
''
'# The ID of the GPU that 'make runtest' will use to run unit tests.'
'TEST_GPUID := 0'
''
'# enable pretty build (comment to see full commands)'
'Q ?= @''
'####################################################################'


Now lets continue with the Ubuntu 15.10 instructions.

Execute the additional commands discussed here:
https://stackoverflow.com/questions/30500977/fails-to-build-caffe-on-ubuntu-15-04

The commands are:

find . -type f -exec sed -i -e 's^"hdf5.h"^"hdf5/serial/hdf5.h"^g' -e 's^"hdf5_hl.h"^"hdf5/serial/hdf5_hl.h"^g' '{}' \;
cd /usr/lib/x86_64-linux-gnu
sudo ln -s libhdf5_serial.so.8.0.2 libhdf5.so
sudo ln -s libhdf5_serial_hl.so.8.0.2 libhdf5_hl.so


Now lets return to the unpacked Caffe directory and enter these commands:

cd python
for req in $(cat requirements.txt); do pip install $req; done


Next, execute:

cd ..
make all
make test
make runtest
make pycaffe      -should be finished already, so you can omit this one
make distribute



* Models download not covered in these instructions. *


----------------------------------------------------------------------------------------------------

****The GPU support prerequisites


In Ubuntu 15.10, enable the use of proprietary drivers in the Software & Updates Center for your desktop and install the NVIDIA graphics driver first from the main Ubuntu package repository.
https://help.ubuntu.com/community/BinaryDriverHowto/Nvidia

Download the CUDA toolkit network installer and the CUDNN package from the NVIDIA site, after registering and filling out the forms.
https://developer.nvidia.com/cuda-downloads

Install the toolkit 7.5 version manually in the terminal as instructed
at the website.

sudo dpkg -i cuda-repo-ubuntu1504_7.5-18_amd64.deb
sudo apt-get update
sudo apt-get install cuda


Download and unpack as root user CUDNN from https://developer.nvidia.com/cudnn.

Put all CUDNN files manually in the path where the CUDA toolkit is, each file in its own respective directory.

Edit the Makefile.config in Caffe directory accordingly and recompile the Caffe. 


----------------------------------------------------------------------------------------
