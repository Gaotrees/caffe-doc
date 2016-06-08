# Faster Caffe Training

Stanford University CS231n Lecture 11 gives useful tips for speeding up your training process:

1. Use LMDB (seek times and no image decompression ie. jpeg).
1. Use cuBLAS. This is a CUDA version of BLAS and will be faster than CPU optimized BLAS.
1. Use cuDNN.
1. Use 32bit floating point precision (when writing new layers), as they compute faster.