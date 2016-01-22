Download OpenCV from http://opencv.org/downloads.html and unpack. Enter the unpacked directory. Execute:


sudo apt-get -y install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip


mkdir build

cd build/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..

make

sudo make install

sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'

sudo ldconfig

sudo apt-get update

reboot the system.


Alternatively, 

sudo apt-get checkinstall

and then instead of "sudo make install" perform the following general command:

sudo checkinstall

while you are in the build directory. 

This will create the OpenCV package that has a modern install/uninstall option.

--------------------------------------------------------------------------------

## Integration with the Caffe

Return to the Caffe directory and perform a cleanup operation with the command

make clean

(Read more here: https://github.com/BVLC/caffe/wiki/Ubuntu-15.10-Installation-Guide)

First, edit the Makefile.config to include the OpenCV library like this...

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial /usr/local/share/OpenCV/3rdparty/lib/

Then, recompile the entire Caffe project.