# Semantic Segmentation

Label each pixel in the image with a category label. Don't differentiate instances, only care about pixels

## Sliding Window

For every pixel, extract a patch centered it and input to CNN to get the label for that pixel.

**Problem**: Very inefficient! Not reusing shared features between overlapping patches.

## Fully Convolutional Network

![](../../img/Learning/DLCV/SS_1.png)

![](../../img/Learning/DLCV/SS_2.png)

## In-Network Upsampleing: "Unpooling"

![alt text](../../img/Learning/DLCV/SS_3.png)

**Bilinear Interpolation**
![alt text](../../img/Learning/DLCV/SS_4.png)

**Bicubic Interpolation**

![alt text](../../img/Learning/DLCV/SS_5.png)

**Max Unpooling**

Pair each downsampling layer with an upsampling layer

When Max Pooling, Remember which position had the max

When Max Unpooling, Place the value into remembered positions, while filling other positions with 0.

**Transposed Convolution**

Convolution with stride > 1 is "Learnable Downsampling"

Can we use stride < 1 for "Learnable Upsampling"?

![](../../img/Learning/DLCV/SS_6.png)

![](../../img/Learning/DLCV/SS_7.png)

![](../../img/Learning/DLCV/SS_8.png)