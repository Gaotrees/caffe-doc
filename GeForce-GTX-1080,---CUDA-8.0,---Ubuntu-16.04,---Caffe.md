#Install cuda 8.0.

As the default gcc in Ubuntu 16.04 is very new, if you have compiling error similar to `#error -- unsupported GNU version! gcc versions later than 5.3 are not supported!`

Try to comment the `#error` line in file `/usr/local/cuda/include/host_config.h`

`#if __GNUC__ > 5 || (__GNUC__ == 5 && __GNUC_MINOR__ > 3)`

`//#error -- unsupported GNU version! gcc versions later than 5.3 are not supported!`

`#endif /* __GNUC__ > 5 || (__GNUC__ == 5 && __GNUC_MINOR__ > 1) */`

#Update nvidia driver

You may need to remove the old driver version installed with cuda-8.0 and install a newer version of driver, if you have error similar to `modprobe: ERROR: could not insert 'nvidia_361_uvm': Invalid argument`

Please refer [here](https://codeyarns.com/2013/02/07/how-to-fix-nvidia-driver-failure-on-ubuntu/) to remove old driver, then install a [new one](http://www.nvidia.com/Download/index.aspx?lang=en-us):

`sudo apt-get purge nvidia-*`

`dkms status`

do this based on your dkms status:

`sudo dkms remove bbswitch/0.8 -k 4.4.0-31-generic`

download the compatible driver (GTX 1080 in my case) from nvidia website and install it

`sudo ./NVIDIA-Linux-x86_64-367.35.run`

reboot if the driver was not updated

`sudo reboot `

compile the sample code and check if it works

`./cuda8-0-samples/bin/x86_64/linux/release/deviceQuery `

#Install prerequisities of Caffe

Because the gcc version is Ubuntu 16.04 is very new, If any prerequisity installed from `apt-get` does not work, uninstall it, compile and install it by the default gcc (5.4) from the source code. The prerequisities that may have problems include: [protobuf](https://github.com/BVLC/caffe/issues/3046) and `opencv`. E.g. if you have protobuf error similar to

`.build_release/lib/libcaffe.so: undefined reference to 'google::protobuf::io::CodedOutputStream::WriteVarint64ToArray(unsigned long long, unsigned char*)'`
Try to uninstall the protobuf installed by `apt-get`, the one installed by apt-get might have been compiled by a older gcc version, so its shared libraries may not be compatible with your default gcc:

`sudo apt-get autoremove libprotobuf-dev protobuf-compiler`

then compile the [protobuf-2.5.0](https://github.com/google/protobuf/tree/v2.5.0) from src and install it. Please config the default gcc (5.4 in my case) when you compile protobuf:

`./configure --prefix=/your/path/ CC=/usr/bin/gcc`

`make`

`make check`

`make install`

#Compile and test Caffe here.