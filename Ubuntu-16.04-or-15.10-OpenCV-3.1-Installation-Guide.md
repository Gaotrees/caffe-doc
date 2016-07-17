## Build
Prepare your Ubuntu system dependencies by executing this command:

    sudo apt-get install --assume-yes libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip

In Ubuntu 16.04, you can resolve dependencies (many are listed below), but the make process will fail at this moment:

    sudo apt-get install build-essential cmake git

    sudo apt-get install ffmpeg libopencv-dev libgtk-3-dev python-numpy python3-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libv4l-dev libtbb-dev qtbase5-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip


Download OpenCV from http://opencv.org/downloads.html and unpack.

Enter the unpacked directory. Execute:

    mkdir build
    cd build/
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..
    make

This completes the building process of OpenCV 3.1. 

### Issues and handling

The make process does not work with Cuda 7.5 and GCC 5 in Ubuntu 16.04. The problem is related to `__mempcpy_inline` and `memcpy` in the `string.h`. To solve this problem one needs to force inlines to CUDA (see [this post](https://github.com/BVLC/caffe/issues/4046) and [this topic](https://github.com/opencv/opencv/issues/6500) for related discussions).

So, run 

    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON -DCUDA_NVCC_FLAGS="-D_FORCE_INLINES" ..
    make

## Installation
### Using `make`
Execute the following:

    sudo make install
    sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
    sudo ldconfig
    sudo apt-get update

and reboot the system.

### Using `checkinstall`

While you are in the build directory, execute these commands:

    sudo apt-get install checkinstall
    sudo checkinstall

This will create the OpenCV package that has a modern install/uninstall option.

--------------------------------------------------------------------------------

## Integration with the Caffe

Return to the Caffe directory and perform a cleanup operation with the command

make clean

(Read more here: https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide)

First, edit the Makefile.config to include the OpenCV 3.1 library like this...

OPENCV_VERSION := 3

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial /usr/local/share/OpenCV/3rdparty/lib/

Then, recompile the entire Caffe project.