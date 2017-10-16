# BLIS
BLIS is a portable software framework for instantiating high-performance BLAS-like dense linear algebra libraries. The framework was designed to isolate essential kernels of computation that, when optimized, immediately enable optimized implementations of most of its commonly used and computationally intensive operations. More about in here: https://github.com/amd/blis

## BLIS is optimized for caffe
The Caffe MNIST benchmark calls GEMM routines for really small matrix sizes. For lot of image processing applications such as hand written digit recognition, the region of interest is usually a smaller subsection of the large image, where the small matrix computation is commonly employed. we have fine tuned the small matrix performance of BLIS for the AMD EPYC processors and we are seeing good performance improvement because of them. You can read more about them here: http://developer.amd.com/wordpress/media/2013/12/Accelerating-Machine-Learning-using-BLIS.pdf

## Linking BLIS with Caffe
Caffe by default does not link with BLIS, hence you need to make modifications in the Makefile to enable it. Just check for the lines in Makefile, where it checks through the list of BLAS libraries (Hint: just search for the line : ifeq ($(BLAS), open)).  

Append the lines in the conditional check:

>
>      else ifeq ($(BLAS), blis)
>         #BLIS
>         LIBRARIES += blis
> 

So after the changes the Makefile will look similar to this:

>
>     #BLAS configuration (default = ATLAS)
>     else ifeq ($(BLAS), open)
>         #OpenBLAS
>          LIBRARIES += openblas
>      else ifeq ($(BLAS), blis)
>          #BLIS
>          LIBRARIES += blis
>      else
>          #ATLAS 

Then in the Makefile.config file, set BLAS := blis and point the BLAS_INCLUDE and BLAS_LIB variables to the installation folder of BLIS. Finally don't forget to set  CPU_ONLY := 1.

Note:
To build BLIS perform the following steps: https://github.com/flame/blis/wiki/BuildSystem.