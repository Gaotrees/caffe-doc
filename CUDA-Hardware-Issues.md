*This is a collection of gossip about versions, hardware, and the like. There is no guarantee of correctness or recency, but if you are having trouble give these hints a try. Your best bet is to refer to the issue tracker.*

**Laboratory Tested Hardware**: Berkeley Vision runs Caffe with k40s, k20s, Titans including models at ImageNet/ILSVRC scale. We have not encountered any trouble in-house with devices with CUDA capability >= 3.0

**CUDA compute capability**: devices with compute capability <= 2.0 may have to reduce CUDA thread numbers and batch sizes due to hardware constraints.

**CUDA driver ver 331.38**: there is a problem with the backwards pass of conv4 that manifests itself as low gpu utilization, a pause, and then the caffe process segfaulting. *Fix*. Downgrade to ver 331.20.