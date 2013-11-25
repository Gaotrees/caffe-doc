Here are a few notes of installation tries on Mac. Just for the record.

(Sergey and Yangqing) Maverick with the most recent clang does not work with caffe yet, due to libc++ problems.

(Sergio): when using OS 10.7.5 Lion, I needed to download OpenCV 2.4.5 instead of the latest, and MKL 2013 instead of the latest.

(Sergio): I got it working in my macbook pro with OS 10.7.5 Lion and Nvidia GT 650 following these steps using Homebrew:
* Install the latest XCode command line tools (for Lion is April 2013)
* brew install glog
* brew tap homebrew/science
* brew install homebrew/science/opencv
* Install MKL 2013 update 5 (The latest 2013 SP1 requires OS 1.8)
* Install CUDA toolkit 5.5
* Update Makefile to point to the right locations
* Once is compiled still need to set DYLD_LIBRARY_PATH for the MKL and CUDA dynamic libraries
* Run all the tests