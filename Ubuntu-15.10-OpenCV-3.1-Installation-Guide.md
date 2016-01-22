Prepare your Ubuntu system dependencies by executing this command:

sudo apt-get -y install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip


Download OpenCV from http://opencv.org/downloads.html and unpack. Enter the unpacked directory. Execute:

mkdir build

cd build/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..

make

This completes the building process of OpenCV 3.1.


READ THE TWO POSSIBLE WAYs TO INSTALL OpenCV 3.1 BELOW and decide which one you like best.

THE DEFAULT WAY TO INSTALL

sudo make install

sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'

sudo ldconfig

sudo apt-get update

reboot the system.


THE ALTERNATIVE WAY TO INSTALL

While you are in the build directory, execute these commands:

sudo apt-get checkinstall

sudo checkinstall

This will create the OpenCV package that has a modern install/uninstall option.

--------------------------------------------------------------------------------

## Integration with the Caffe

Return to the Caffe directory and perform a cleanup operation with the command

make clean

(Read more here: https://github.com/BVLC/caffe/wiki/Ubuntu-15.10-Installation-Guide)

First, edit the Makefile.config to include the OpenCV 3.1 library like this...

OPENCV_VERSION := 3

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial /usr/local/share/OpenCV/3rdparty/lib/

Then, recompile the entire Caffe project.