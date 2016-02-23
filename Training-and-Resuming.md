# Training and Resume

In caffe, during training files defining the state of the network will be output: .caffemodel and .solverstate. These two files define the current state of the network at a given iteration, and with this information we are able to continue training our network in the case of a hiccup, pause for diagnosis, or a system crash.

## Training

To begin training, we simply need to call the caffe binary and supply a solver:
`caffe train -solver solver.prototxt`

## Stopping

### Number of Iterations Limit

### Manually Stopping

# Resuming