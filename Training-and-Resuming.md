# Training and Resuming

In caffe, during training files defining the state of the network will be output: .caffemodel and .solverstate. These two files define the current state of the network at a given iteration, and with this information we are able to continue training our network in the case of a hiccup, pause for diagnosis, or a system crash.

## Training

To begin training, we simply need to call the caffe binary and supply a solver:

`caffe train -solver solver.prototxt`

## Stopping

### Number of Iterations Limit

We can have our network stop after a specified number of iterations with a parameter in the solver.prototxt named `max_iter`. 

For example, we can specify that we would like our network to stop after 60,000 iteration, thus we set the parameter accordingly: `max_iter: 60000`.

### Manually Stopping

It is possible to manually stop a network from training by pressing the `Ctrl+C` key combination.
By default, a snapshot will be saved when training is stopped manually.
This behavior can be changed by flags `sigint_effect` (for [SIGINT](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGINT) signal) and `sighup_effect` (for [SIGHUP](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGHUP)), see `caffe --help`.
Default behavior for `sigint_effect` (emitted by Ctrl+C on Linux) is `"stop"`, which might also cause a snapshot save, because the Solver itself [can be configured](https://github.com/BVLC/caffe/blob/c32629435a1e5dacc8a90a309d8b255d7b629379/src/caffe/solver.cpp#L310-L313) to save after the training ends - either normally or by interruption.
The default setting of `snapshot_after_train` is `true` - see [caffe.proto](https://github.com/BVLC/caffe/blob/c32629435a1e5dacc8a90a309d8b255d7b629379/src/caffe/proto/caffe.proto#L228).

**Note about `tee`:** if you redirect Caffe output with `tee`, for example by calling  
`caffe train -solver=solver.txt -gpu=0 2>&1 | tee output.log`  
you might notice Caffe *not* saving a snapshot on Ctrl+C.
This is because when you input Ctrl+C, you actually send the interrupt signal to the `tee` process, not Caffe.
And it just turns out that when `tee` is interrupted, it sends a SIGKILL to the underlying process.
A way to work around this is to check the ID of Caffe process (hint: read the log - PID is the number right before the filename) and manually sending a signal to Caffe itself, e.g. `kill -s SIGINT <caffe_pid>`.

# Resuming

When a network has stopped training, either due to manual halting or by reaching the maximum iterations, we may continue training our network by telling caffe to train from where we left off. This is as simple as supplying the snapshot flag with the current .solverstate file. For example:

`caffe train -solver solver.prototxt -snapshot train_190000.solverstate`

In this case we will continue training from iteration 190000.