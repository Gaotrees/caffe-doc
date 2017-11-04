# Training and Resuming

In caffe, during training files defining the state of the network will be output: .caffemodel and .solverstate. These two files define the current state of the network at a given iteration, and with this information we are able to continue training our network in the case of a hiccup, pause for diagnosis, or a system crash.

## Training

To begin training, we simply need to call the caffe binary and supply a solver:

`caffe train -solver solver.prototxt`

## Stopping

### Number of Iterations Limit

We can have our network stop after a specified number of iterations with a parameter in the solver.prototxt named `max_iter`. 

For example, we can specify that we would like our network to stop after 60,000 iteration, thus we set the parameter accordingly: `max_iter: 600000`.

### Manually Stopping

It is possible to manually stop a network from training by pressing the `Ctrl+C` key combination. When the stop signal is sent, the network will halt the forward and backwards pass, and output the current state of the network in a .caffemodel and .solverstate titled with the current iteration number.

# Resuming

When a network has stopped training, either due to manual halting or by reaching the maximum iterations, we may continue training our network by telling caffe to train from where we left off. This is as simple as supplying the snapshot flag with the current .solverstate file. For example:

`caffe train -solver solver.prototxt -snapshot train_190000.solverstate`

In this case we will continue training from iteration 190000.