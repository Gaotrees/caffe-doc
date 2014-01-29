Refer to the project's issue tracker for [hardware/compatibility](https://github.com/BVLC/caffe/issues?labels=hardware%2Fcompatibility&page=1&state=open).

**Laboratory Tested Hardware**: Berkeley Vision runs Caffe with k40s, k20s, Titans including models at ImageNet/ILSVRC scale. We have not encountered any trouble in-house with devices with CUDA capability >= 3.0

**CUDA compute capability**: devices with compute capability <= 2.0 may have to reduce CUDA thread numbers and batch sizes due to hardware constraints. Your mileage may vary.