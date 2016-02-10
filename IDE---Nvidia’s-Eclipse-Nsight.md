# Nsight Eclipse Edition

Nsight Eclipse is a tool made by NVidia to assist in edditing, building, debugging Cuda applications. It is avaible on the NVidia developer site at: https://developer.nvidia.com/nsight-eclipse-edition

## Creating a caffe Project

1. Launch Nsight.
1. Navigate to File -> New -> Makefile Project with Existing Code.
1. Name your project caffe, or something of your choosing.
1. Under existing code location, select the browse button.
1. Navigate to your caffe directory.
1. Select OK.
1. Select Finish.
1. Open the caffe Makefile.config and uncomment the debug line: `DEBUG := 1`.

## Building caffe and tests

### Building caffe

1. Select the hammer icon in the top menu bar. It should work out of the box.

### Building Tests

1. In the Make Target Pane, right-click and select `New...`
1. Name the target `build_test`.
1. Clear the Make Target field.
1. In the Build Command field enter `make test -j <Number of cores that you have>`

### Running All Tests

1. In the Make Target Pane, right-click and select `New...`
1. Name the target `run_all_tests`.
1. Clear the Make Target field.
1. In the Build Command field enter `make runtest`