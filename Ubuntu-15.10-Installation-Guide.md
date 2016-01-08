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

The following configuration example uses CPU only for the computations. Change it accordingly if you have an NVIDIA graphics card with the proprietary driver, CUDA toolkit and CUDNN installed on a real, physical machine. (Unable to display the entire file.) It should contain the following lines.


PYTHON_INCLUDE := /usr/include/python2.7 /usr/lib/python2.7/dist-packages/numpy/core/include
WITH_PYTHON_LAYER := 1
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include /usr/include/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial


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
