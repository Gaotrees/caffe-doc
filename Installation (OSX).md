# OSX 10.9

The installation instructors provided on the official page should work in most cases. If you were not able to get them to work, the instructions here might be of help. Any packages you can install with Homebrew, you should, for ease of maintenance and installation. 

1. Install dependencies

    1. [CUDA](https://developer.nvidia.com/cuda-downloads). Even if your machine does not have a GPU, the CUDA libraries / headers need to be found by Caffe. Had success with CUDA 6.5.
    2. BLAS. On OSX 10.9, BLAS is provided by the Accelerate / vecLib framework natively by Apple. But when running the caffe tests, there is some numerical instability using those BLAS libraries. As a workaround, install the MKL from Intel using a [student](https://software.intel.com/en-us/intel-education-offerings) license. Make sure you take note of the install directories. By default, they will be installed in `/opt/intel/`, but you can specify that in the installation process. Make sure that during the installation you install all the packages necessary for the Intel MKL toolbox - by default, some options are unchecked. Had success with the Composer XE 2015.0.077 toolbox version. 

2. Homebrew dependencies

Follow all the instructions on the [official installation](http://caffe.berkeleyvision.org/installation.html) page (editing all the install files) with one modification: when you get to installing Boost, version 1.56 sometimes has the numerical instability issue. Try installing Boost 1.55 instead: 

```
cd /usr/local
git checkout a252214 /usr/local/Library/Formula/boost.rb
brew install --build-from-source --with-python --fresh -vd boost
```

# Miscellaneous hints

* If you get compile errors with openBLAS and ATLAS (which are more likely) and end up using MKL, make sure to add all the MKL libraries to your path. The default install directory for MKL is `/opt/intel/mkl`, and on my system I had to add to a number of environment variables to get MKL to load with Caffe: 

```
export MKLROOT=/opt/intel/composer_xe_2015.0.077/mkl export DYLD_LIBRARY_PATH=/opt/intel/composer_xe_2015.0.077/compiler/lib:/opt/intel/composer_xe_2015.0.077/mkl/lib export LIBRARY_PATH=/opt/intel/composer_xe_2015.0.077/compiler/lib:/opt/intel/composer_xe_2015.0.077/mkl/lib export NLSPATH=/opt/intel/composer_xe_2015.0.077/mkl/lib/locale/%l_%t/%N export MANPATH=/opt/intel/composer_xe_2015.0.077/man/en_US:/usr/local/share/man:/usr/share/man:/opt/intel/man:/usr/texbin/man:$ export INCLUDE=/opt/intel/composer_xe_2015.0.077/mkl/include export CPATH=/opt/intel/composer_xe_2015.0.077/mkl/include:/opt/intel/composer_xe_2015.0.077/mkl/bin/intel64/mklvars_intel64.sh
```

* Make absolutely sure that you are using the same Python for building all the necessary homebrew Python dependencies as you will be using Python. If you installed Python with homebrew rather than Anaconda, make sure you linked it. Reference this great how-to guide: http://docs.python-guide.org/en/latest/starting/install/osx/