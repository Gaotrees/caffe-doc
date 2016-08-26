The official [installation instructions](http://caffe.berkeleyvision.org/installation.html) explain the recommended steps for installing on the official platforms of Ubuntu 14.04 and 12.04 and OS X 10.10, 10.9, and 10.8.

These unofficial instructions collect tips and guides but without any guarantees. Please add any missing details and correct any mistakes.

## Linux
- [[Ubuntu 14.04/Cuda 7 for EC2|Caffe-on-EC2-Ubuntu-14.04-Cuda-7]]: AMI and installation script that works on EC2 g2.2xlarge and g2.8xlarge instances.
- [[Ubuntu 14.04 VirtualBox VM|Ubuntu-14.04-VirtualBox-VM]]: virtual machine installation with CUDA 6.5 and system Python.
- [[Ubuntu 14.04 ec2 instance|Ubuntu-14.04-ec2-instance]]: ec2 installation with CUDA 6.5 and video walkthrough plus a vagrant VM. (Needs update for latest Caffe).
- [Docker image (GPU only)](https://registry.hub.docker.com/u/tleyden5iwx/caffe-gpu-master/): a Docker image for GPU mode, including Python dependencies.  For detailed instructions, see [Running Caffe on AWS GPU Instance via Docker](http://tleyden.github.io/blog/2014/10/25/running-caffe-on-aws-gpu-instance-via-docker/)
- [Docker image (CPU only)](https://registry.hub.docker.com/u/tleyden5iwx/caffe-cpu-master/): Same as above, but CPU only.
- [Alt. CPU Docker image](https://hub.docker.com/r/kaixhin/caffe/): Weekly builds of Caffe (CPU-only).
- [Alt. GPU Docker image](https://hub.docker.com/r/kaixhin/cuda-caffe/): Weekly builds of Caffe (CUDA 6.5, 7.0 and 7.5 versions available). See [source project](https://github.com/Kaixhin/dockerfiles) for details.
- [Super computing cluster without root access (GPU+CPU)](http://andrewjanowczyk.com/installing-caffe-on-the-ohio-super-computing-osc-ruby-cluster/): Cuda 6.5, cuDNN V1, Python 2.7.x 

## OS X

See the official instructions.

## Windows
The official windows port can be accessed from [Microsoft/caffe](https://github.com/Microsoft/caffe), which is supported by Microsoft. 

There is an unofficial Windows port of Caffe at [niuzhiheng/caffe:windows](https://github.com/niuzhiheng/caffe). Thanks @niuzhiheng!

Another unofficial Windows port of Caffe at [redknightlois/caffe] (https://github.com/redknightlois/caffe). This port is based on work done by @initialneal. Binary packages to compile available at: https://initialneil.wordpress.com/2015/01/11/build-caffe-in-windows-with-visual-studio-2013-cuda-6-5-opencv-2-4-9/

Yet another unofficial Windows port can be found at [willyd/caffe](https://github.com/willyd/caffe). Unlike the previous ports this one builds on top of the CMake build. A super-build project that downloads and builds all Caffe dependencies is also available at [willyd/caffe-builder](https://github.com/willyd/caffe-builder.git). 



