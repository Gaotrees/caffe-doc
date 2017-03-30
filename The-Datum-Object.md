# Datum

Datum is a Google Protobuf Message class used to store data and optionally a label. A Datum can be thought of a as a matrix with three dimensions: width, height, and channel.

## Simple Example

In this example, we will create a simple Datum, set three input values, and set the label.

```C++
Datum datum;
datum.set_width(3); // our data has three inputs
datum.set_height(1); // our data is one-dimensional
datum.set_channels(1);

google::protobuf::RepeatedField<float>* datumFloatData = datum.mutable_float_data();
datumFloatData->Add(0.0f);
datumFloatData->Add(1.0f);
datumFloatData->Add(0.0f);

datum.set_label(2);
``` 

## Common Usage

Datum is often used in a data layer as an intermediate object which helps facilitate setting the batch's data and label (which correspond to the top blobs).