This is a guide to setting up Caffe in a 14.04 virtual machine with CUDA 6.5 and the system Python for getting started with examples and PyCaffe.

* Download newest Ubuntu release. I used KUbuntu from http://cdimage.ubuntu.com/kubuntu/releases/trusty/release/kubuntu-14.04.1-desktop-amd64.iso
* Start VirtualBox, create a new virtual machine (Linux/Ubuntu/64bit/DynamicHD/8GbRAM/…). Then start the VM from the downloaded .iso (do this from inside VirtualBox). Installation of Kubuntu will begin.
* Install system updates (3.13.0-32 -> 3.13.0-36)
* Install build essentials:
  * `sudo apt-get install build-essential`
* Install latest version of kernel headers:
  * ``sudo apt-get install linux-headers-`uname -r` ``
* Install VBox Additions:
  * Click the USB icon in the task-bar (lower right of screen)
  * Left click the VBOXADDITIONS_4.3.16_95972
  * Select “Open with File Manager” (this will mount the virtual CD in the virtual CD drive…). Once the file manager window has opened, you can kill it. This step is only needed to mount the CD...
  * `cd /media/<USER>/VBOXADDITIONS_4.3.16_95972` (where `<USER>` is your user name)
  * `sudo ./VBoxLinuxAdditions.run`
* Activate bidirectional clip-board:
  * In Virtual Box Manager, click Settings, then General | Advanced | Shared Clipboard
* Install curl (for the CUDA download):
  * `sudo apt-get install curl`
* Download CUDA.
  * `cd ~/Downloads/`
  * `curl -O "http://developer.download.nvidia.com/compute/cuda/6_5/rel/installers/cuda_6.5.14_linux_64.run"`
* Make the downloaded installer file runnable:
  * `chmod +x cuda_6.5.14_linux_64.run`
* Run the CUDA installer:
  * ``sudo ./cuda_6.5.14_linux_64.run --kernel-source-path=/usr/src/linux-headers-`uname -r`/ ``
    * Accept the EULA
    * Do **NOT** install the graphics card drivers (since we are in a virtual machine)
    * Install the toolkit (leave path at default)
    * Install symbolic link
    * Install samples (leave path at default)
* Update the library path
  * `echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc`
  * `echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/lib' >> ~/.bashrc`
  * `source ~/.bashrc`
* Install dependencies:
  * `sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip libgoogle-glog-dev libbz2-dev libxml2-dev libxslt-dev libffi-dev libssl-dev libgflags-dev liblmdb-dev python-yaml`
  * `sudo easy_install pillow`
* Download Caffe:
  * `cd ~`
  * `git clone https://github.com/BVLC/caffe.git`
* Install python dependencies for Caffe:
  * `cd caffe`
  * `cat python/requirements.txt | xargs -L 1 sudo pip install`
* Add a couple of symbolic links for some reason:
  * `sudo ln -s /usr/include/python2.7/ /usr/local/include/python2.7`
  * `sudo ln -s /usr/local/lib/python2.7/dist-packages/numpy/core/include/numpy/ /usr/local/include/python2.7/numpy`
* Create a `Makefile.config` from the example:
  * `cp Makefile.config.example Makefile.config`
  * `nano Makefile.config`
    * Uncomment the line `# CPU_ONLY := 1`  (In a virtual machine we do not have access to the the GPU)
    * Under `PYTHON_INCLUDE`, replace `/usr/lib/python2.7/dist-packages/numpy/core/include` with `/usr/local/lib/python2.7/dist-packages/numpy/core/include` (i.e. add `/local`)
* Compile Caffe:
  * `make pycaffe`
  * `make all`
  * `make test`
* Download the ImageNet Caffe model and labels:
  * `./scripts/download_model_binary.py models/bvlc_reference_caffenet`
  * `./data/ilsvrc12/get_ilsvrc_aux.sh`
* Modify `python/classify.py` to add the `--print_results` option
  * Compare `https://github.com/jetpacapp/caffe/blob/master/python/classify.py` (version from 2014-07-18) to the current version of `classify.py` in the official Caffe distribution `https://github.com/BVLC/caffe/blob/master/python/classify.py` 

* Test your installation by running the ImageNet model on an image of a kitten:
  * `cd ~/caffe` (or whatever you called your Caffe directory)
  * `python python/classify.py --print_results examples/images/cat.jpg foo`
  * Expected result: `[('tabby', '0.27933'), ('tiger cat', '0.21915'), ('Egyptian cat', '0.16064'), ('lynx', '0.12844'), ('kit fox', '0.05155')]`
  * If running this command results in `ValueError: Mean shape incompatible with input shape.` in `python/caffe/io.py`, modify `python/caffe/io.py` as follows:
 
````
# Replace this
if ms != self.inputs[in_][1:]:`
    raise ValueError('Mean shape incompatible with input shape.')
```
```
# With this
if ms != self.inputs[in_][1:]:
    print(self.inputs[in_])
    in_shape = self.inputs[in_][1:]
    m_min, m_max = mean.min(), mean.max()
    normal_mean = (mean - m_min) / (m_max - m_min)
    mean = resize_image(normal_mean.transpose((1,2,0)),in_shape[1:]).transpose((2,0,1)) * (m_max - m_min) + m_min
    #raise ValueError('Mean shape incompatible with input shape.')
```
  [Source](https://stackoverflow.com/questions/30808735/error-when-using-classify-in-caffe), [Explanation](https://stackoverflow.com/questions/28692209/using-gpu-despite-setting-cpu-only-yielding-unexpected-keyword-argument/28979649#28979649)

* Test your installation by training a net on the MNIST dataset of handwritten digits:
  * `cd ~/caffe` (or whatever you called your Caffe directory)
  * `./data/mnist/get_mnist.sh`
  * `./examples/mnist/create_mnist.sh`
  * Now edit `./examples/mnist/lenet_solver.prototxt` and change `solver_mode` from `GPU` to `CPU`
  * `./examples/mnist/train_lenet.sh`
  * See http://caffe.berkeleyvision.org/gathered/examples/mnist.html for more information...
  * To get most of the bash commands given in this page as a shell script to speed up installation see https://github.com/abhishekraok/promising-patterns/blob/master/CaffeUbuntuVMInstall.sh