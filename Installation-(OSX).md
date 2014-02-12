See the [OS X installation section of the online documentation](http://caffe.berkeleyvision.org/installation.html#os_x_installation).

- 10.7: works
- 10.8: works
- 10.9: works with strenuous building and linking, at least until the next CUDA release (due to libstc++ linking).

**10.7.5 notes by Sergio.**
Caffe works with OS X 10.7.5 and an NVIDIA GT 650 following these steps using Homebrew:
* Install the latest XCode command line tools (for Lion is April 2013)
* brew install glog
* brew tap homebrew/science
* brew install homebrew/science/opencv
* Install MKL 2013 update 5 (The latest 2013 SP1 requires OS 1.8)
* Install CUDA toolkit 5.5
* Update Makefile to point to the right locations
* Once is compiled still need to set DYLD_LIBRARY_PATH for the MKL and CUDA dynamic libraries
* Run all the tests