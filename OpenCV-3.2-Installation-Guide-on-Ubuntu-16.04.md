## How to Build OpenCV 3.2

In Ubuntu 16.04, install the dependencies first and then build the OpenCV 3.2 from source. 

```
sudo apt-get install --assume-yes build-essential cmake git
sudo apt-get install --assume-yes pkg-config unzip ffmpeg qtbase5-dev python-dev python3-dev python-numpy python3-numpy
sudo apt-get install --assume-yes libopencv-dev libgtk-3-dev libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev
sudo apt-get install --assume-yes libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev
sudo apt-get install --assume-yes libv4l-dev libtbb-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev
sudo apt-get install --assume-yes libvorbis-dev libxvidcore-dev v4l-utils python-vtk
sudo apt-get install --assume-yes liblapacke-dev libopenblas-dev checkinstall
sudo apt-get install --assume-yes libgdal-dev
```

In order to install the NVIDIA Cuda Toolkit with CUDNN library, see https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide#the-gpu-support-prerequisites 

Download the latest source archive for OpenCV 3.2 from https://github.com/opencv/opencv/archive/3.2.0.zip

Enter the unpacked directory. Execute:

    mkdir build
    cd build/    
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D FORCE_VTK=ON -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D WITH_CUBLAS=ON -D CUDA_NVCC_FLAGS="-D_FORCE_INLINES" -D WITH_GDAL=ON -D WITH_XINE=ON -D BUILD_EXAMPLES=ON ..
    make -j $(($(nproc) + 1))

This completes the build procedure of OpenCV 3.2. (http://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html)


## Installation
### Using `make`
Execute the following:

    sudo make install
    sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
    sudo ldconfig
    sudo apt-get update

and reboot the system.

### Using `checkinstall` (this gives incomplete results without the installation by using ```make```)

While you are in the build directory, execute these commands:

    sudo apt-get install checkinstall
    sudo checkinstall

Fill in the text as required to give the description and the package name. This will create the OpenCV 3.2 package that has a modern install/uninstall option.

--------------------------------------------------------------------------------

## Integration with the Caffe

Return to the Caffe directory and perform a cleanup operation with the command

make clean

(Read more here: https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide)

First, edit the Makefile.config to include the OpenCV 3.2 library like this...

OPENCV_VERSION := 3

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial /usr/local/share/OpenCV/3rdparty/lib/

Then, recompile the entire Caffe project.
