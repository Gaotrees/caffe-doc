# The Data Layer

A data layer is generally the first layer of any network. The data layer is exactly like any other layer except that it has a very special task: shaping and populating the initial blobs that will traverse the network. The data layer has no backward pass, as it is not responsible for any error produced in the network.

## Blob Shape and Blob Data

Blobs are defined by two pieces of information: their shape, and the data they contain. A blob's shape is it's physical dimensions, whereas a blob's data is the values at each index in the blob. As a subclasser of the `BaseDataLayer` or more accurately (`BasePrefetchingDataLayer`), you are required to implement two methods: `DataLayerSetUp`, and `load_batch`, along side the constructor, destructor, and blob count methods.

### DataLayerSetUp

The `DataLayerSetup` method is responsible for setting up the data layer. This method implementation generally initializes all of your parameters, and defines the shape of the `top` blobs.

### load_batch(Batch<Dtype>* batch)

The `load_batch` method is responsible for generating the data. This method implementation generally loads, loads and modifies, or generates new pieces of data. The data is then to be stored in the cpu or gpu data for later processing.

## The Data Layer Has Power

The data layer's duty is to feed the network a blob of data. The data layer can perform an unlimited number of alterations to this piece of data before passing it off to the next layer. These alterations can be done in-line, meaning no altered versions of the data have to be stored on a hard drive. With each pass of the data layer we can manipulate any single piece of data, or even create data from scratch.

### Example: Data Augmentation

Data augmentation is a technique used to add variation to the data, for example one might augment an image through rotations, scales, additive brightness changes, and multiplicative brightness changes. The technique of data augmentation has been shown to enrich the data and add more invariance to a network.

Let's say we are working with a data set consisting of 100 images. Assuming that those images are horizontally, vertically, and rotationally valid (they still have meaning with these alterations), then we can treat each image as many images by applying exactly these kinds of manipulations. With a simply horizontal flip, we can double the amount of data we are working with. Compounding a vertical flip, we have essentially doubled the number of examples the network will see. Even without the rotation, we have quadrupled our data set to 400 images.