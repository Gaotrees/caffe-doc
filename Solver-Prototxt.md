The solver.prototxt is a configuration file used to tell caffe how you want the network trained.

## Parameters

#### base_lr  

This parameter indicates the base (beginning) learning rate of the network. The value is a real number (floating point).

#### lr_policy

This parameter indicates how the learning rate should change over time.

Options include:
1. step - drop the learning rate in step sizes indicated by the gamma parameter.

#### gamma

This parameter indicates how much the learning rate should change every time we reach the next "step." The value is a real number, and can be though of as multiplying the current learning rate by said number to gain a new learning rate.

#### stepsize

This parameter indicates how often (at some iteration count) that we should move onto the next "step" of training. This value is a positive integer.

#### max_iter

This parameter indicates when the network should stop training. The value is an integer indicate which iteration should be the last.

#### momentum

This parameter indicates how much of the previous weight will be retained in the new calculation. This value is a real fraction.

#### solver_mode

This parameter indicates which mode will be used in solving the network.

Options include:
1. CPU
1. GPU