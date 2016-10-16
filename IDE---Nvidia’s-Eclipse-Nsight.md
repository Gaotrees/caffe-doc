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

Select the hammer icon in the top menu bar. It should work out of the box.

### Building Tests

1. In the Make Target Pane, right-click and select `New...`
1. Name the target `build_test`.
1. Clear the Make Target field.
1. In the Build Command field enter `make test -j`

When this is complete, the Make Target Pane should have a target named `build_test`. Double click build your tests.

### Running All Tests

1. In the Make Target Pane, right-click and select `New...`
1. Name the target `run_all_tests`.
1. Clear the Make Target field.
1. In the Build Command field enter `make runtest`

When this is complete, the Make Target Pane should have a target named `run_all_tests`. Double click this to run all of your tests.

## Debugging

### First Time

1. Ensure that you've built everything (the code and the tests).
1. Click the bug icon in the top menu.
1. You will be presented with a list of bin objects.
1. Select the one you want to debug.

### Second Time and on (if you don't want to debug the same bin)

1. Select the little arrow beside the bug icon.
1. Select `Debug Configurations...`.
1. Under the Main tab, select Search Project.
1. Select the new bin you want to debug.

## Some additional references
http://www.pittnuts.com/2015/06/build-and-debug-caffe-in-nsight/