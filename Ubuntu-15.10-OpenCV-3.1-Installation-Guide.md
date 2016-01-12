Download OpenCV from http://opencv.org/downloads.html and unpack. Enter the unpacked directory. Execute:


sudo apt-get -y install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip


mkdir build

cd build/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..

make

sudo make install

sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'

sudo ldconfig

-------------------------------------------------------------------------------------------------------------

Caffe can be compiled with the OpenCV version 3.1, but this version needs to be denoted in the Caffe's own Makefile.config. Enter the base directory of the unpacked Caffe source and edit the Makefile.config

 Uncomment if you're using OpenCV 3

 OPENCV_VERSION := 3

Recompile...

See https://github.com/BVLC/caffe/wiki/Ubuntu-15.10-Installation-Guide

--------------------------------------------------------------------------------------------------------------
NOTE: if the system was updated, perhaps the Python layer needs to be updated, because the Python module no longer works.

cd python

for req in $(cat requirements.txt); do pip install $req; done

In case of any problems, try:

for req in $(cat requirements.txt); do sudo -H pip install $req --upgrade; done

cd ..

--------------------------------------------------------------------------------------------------------------



make clean

make all


optional:

make pycaffe

make distribute

make tests

make runtests


