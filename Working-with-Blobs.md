# Blob

Blob is a variable dimension sized data structure.

## The Common Way to Look At It

A Blob is generally used as a four dimensional ordered data structure: number, channels, height, and width.

The channels, height, and width usually describe a piece of data such as an image - RGB by Width by Height - but isn't limited to images. Throughout the network a Blob will often be various sizes as it may represent some high dimensional (large number of channels) set of feature vectors.

## Working With the Blob

### Getting Data from a Blob

A piece of data can be retrieved from the blob via the data_at(vector<int>& index) or the data_at(int number, int channels, int height, int width) methods. 

For example, the following code will check that the label from the first batch element, at the first channel, first height index, and first width index is equal to 1.

```C++
CHECK_EQ(blob_top_label_->data_at(0,0,0,0), 1);
```