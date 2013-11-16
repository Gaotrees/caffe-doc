RBG's install log
---

0) Get code
$ git clone git@github.com:Yangqing/caffe.git
$ cd caffe

1) Edited ./Makefile 
  A) Use local include (not sure why I did it this way...):
    INCLUDE_DIRS := ./local/include ...
    LIBRARY_DIRS := ./local/lib ...


  B) Hack Makefile to point to where python is installed on my system:

  pycaffe: $(STATIC_NAME) python/caffe/pycaffe.cpp $(PROTO_GEN_PY)
      protoc --proto_path=src --python_out=python $(PROTO_SRCS)
      $(CXX) -o python/caffe/pycaffe.so -I/opt/py/anaconda/include/python2.7 \
          -I/opt/py/anaconda/lib/python2.7/site-packages/numpy/core/include/ -shared \
          python/caffe/pycaffe.cpp $(STATIC_NAME) $(CXXFLAGS) $(LDFLAGS) \
          $(WARNING) -lboost_python -lpython2.7

2) Try to build it
$ make
... failed ...
In file included from src/caffe/proto/caffe.pb.cc:4:0:
./src/caffe/proto/caffe.pb.h:9:42: fatal error: google/protobuf/stubs/common.h: No
compilation terminated.
...

3) Install google protocol buffer
$ sudo apt-get install libprotobuf-dev
$ make
... failed ...
In file included from ./include/caffe/blob.hpp:6:0,
                 from src/caffe/blob.cpp:6:
                 ./include/caffe/common.hpp:12:26: fatal error: glog/logging.h: No
                 compilation terminated.
...

4) Install google logging library
$ wget https://google-glog.googlecode.com/files/glog-0.3.3.tar.gz
$ tar zxvf glog-0.3.3.tar.gz
$ ./configure --prefix=/home/rbg/working/caffe/local
$ make
$ make install

5) Failed because of no MKL
$ ... install intel MKL ...
$ make
... failed ...
In file included from src/caffe/layer_factory.cpp:9:0:
./include/caffe/vision_layers.hpp:6:24: fatal error: leveldb/db.h: No such file or directory
...

6) Install leveldb
$ sudo apt-get install libleveldb-dev
$ make
... failed ...
src/caffe/util/io.cpp:8:33: fatal error: opencv2/core/core.hpp: No such file or directory
compilation terminated.
make: *** [src/caffe/util/io.o] Error 1
...

7) Install OpenCV
$ ... install opencv 2.4.7 from source ...
$ make
... failed ...
/usr/bin/ld: cannot find -lsnappy
collect2: ld returned 1 exit status
...

8) Install libsnappy
$ make
... failed ...
-lboost_python -lpython2.7
/usr/bin/ld: cannot find -lboost_python
collect2: ld returned 1 exit status
make: *** [pycaffe] Error 1
...

9) Install libboost python
$ sudo apt-get install libboost-python1.48-dev
$ make
... SUCCESS!!! ...

# Library path required
export LD_LIBRARY_PATH=./local/lib:/opt/intel/mkl/lib/intel64:/usr/local/cuda/lib64