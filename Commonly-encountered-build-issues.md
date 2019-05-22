This page attempts to collect a list of commonly encountered build issues and provide solutions to them. Since it is mostly community-maintained, it is by far not comprehensive - you're encouraged to make edits, adding new answers and correcting mistakes. Links to existing answers (e.g. on [caffe-users](https://groups.google.com/forum/#!forum/caffe-users) or [StackOverflow](https://stackoverflow.com/questions/tagged/caffe)) are welcome!

### 1) HDF5 issues:
**Problem**:
```
src/caffe/net.cpp:8:18: fatal error: hdf5.h: No such file or directory
compilation terminated.
Makefile:581: recipe for target '.build_release/src/caffe/net.o' failed
make: *** [.build_release/src/caffe/net.o] Error 1
```

**or**

```
AR -o .build_release/lib/libcaffe.a
LD -o .build_release/lib/libcaffe.so.1.0.0
/usr/bin/ld: cannot find -lhdf5_hl
/usr/bin/ld: cannot find -lhdf5
collect2: error: ld returned 1 exit status
Makefile:572: recipe for target '.build_release/lib/libcaffe.so.1.0.0' failed
make: *** [.build_release/lib/libcaffe.so.1.0.0] Error 1
```
**Solution**:
 * install `libhdf5-dev`
 * open Makefile.config, locate line containing `LIBRARY_DIRS` and append `/usr/lib/x86_64-linux-gnu/hdf5/serial`. Please note the space rather than a colon for defining path
 * locate `INCLUDE_DIRS` and append `/usr/include/hdf5/serial/` (per [this SO answer](https://askubuntu.com/a/645089/599356))
 * rerun `make all`
   
### 2) gflags issues:
**Problem**:
```
In file included from src/caffe/net.cpp:10:0:
./include/caffe/common.hpp:5:27: fatal error: gflags/gflags.h: No such file or directory
compilation terminated.
Makefile:581: recipe for target '.build_release/src/caffe/net.o' failed
make: *** [.build_release/src/caffe/net.o] Error 1
```
**Solution**: Run `sudo apt-get install libgflags-dev`. Then rerun `make all`.

### 3) glog issues:
**Problem**:
```
In file included from src/caffe/net.cpp:10:0:
./include/caffe/common.hpp:6:26: fatal error: glog/logging.h: No such file or directory
compilation terminated.
Makefile:581: recipe for target '.build_release/src/caffe/net.o' failed
make: *** [.build_release/src/caffe/net.o] Error 1
```
**Solution**: Run `sudo apt-get install libgoogle-glog-dev`. Then rerun `make all`.

### 4) LMDB issues:
**Problem**:
```
In file included from src/caffe/util/db.cpp:3:0:
./include/caffe/util/db_lmdb.hpp:8:18: fatal error: lmdb.h: No such file or directory
compilation terminated.
Makefile:581: recipe for target '.build_release/src/caffe/util/db.o' failed
make: *** [.build_release/src/caffe/util/db.o] Error 1
```
**Solution**: Run `sudo apt-get install liblmdb-dev`. Then rerun `make all`.

### 5) opencv_imgcodecs opencv_videoio issues:
**Problem**:
```
/usr/bin/ld: cannot find -lopencv_imgcodecs
/usr/bin/ld: cannot find -lopencv_videoio
collect2: error: ld returned 1 exit status
Makefile:579: recipe for target '.build_release/lib/libcaffe.so.1.0.0-rc5' failed
make: *** [.build_release/lib/libcaffe.so.1.0.0-rc5] Error 1
```
**Solution**: open your Makefile (NOT Makefile.config!) with some text editor, locate line 164 (in my case), add opencv_imgcodecs below it.
```
LIBRARIES += glog gflags protobuf leveldb snappy \
  lmdb boost_system hdf5_hl hdf5 m \
  opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs
```