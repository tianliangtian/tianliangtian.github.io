# Convolutional Network
* **Problem**: So far our classifiers don't respect the spatial structure of images!

* **Solution**: Define new computational nodes that operate on images!


![](../img/Learning/DLCV/CN_1.png)

## Convolutional Layer
![](../img/Learning/DLCV/CN_c1.png)

* There can be many filters generating many activation maps.
* Each filter must have same depth as the input image.
* Each filter also has a bias.
* Activation map can be considered as a feature vector, telling us the structure of the input.

![](../img/Learning/DLCV/CN_7.png)

* The input is often a batch of images
* The output channel $C_{out}$ is usually different from input channel $C_{in}$

![](../img/Learning/DLCV/CN_c2.png)

## Pooling Layer
* Compute one unique number to represent the region to downsampling.

![](../img/Learning/DLCV/CN_c3.png)

## Convolutional Network Architecture

![](../img/Learning/DLCV/CN_c4.png)

## Normalization

* **Problem**: Deep network is hard to train
* Normalization is introduced to accelerate optimization.

![](../img/Learning/DLCV/CN_c5.png)

* The batch normalization get its name for it doing normalization in batch dimension $N$. 
* It's a stiff constraint for those layers to exactly fit zero mean and unit variance. So in practice, we introduce learnable scale and shift $\gamma,\beta$ to make our network able to learn mean and variance.

![](../img/Learning/DLCV/CN_c6.png)

* It is wired that the result of one image is influenced by other images, so the model process differently in training time and test time
    * **Training Time**: empirically compute mean and variance.
    * **Test Time**: use the average of historical mean and variance computed during training to compute.

![](../img/Learning/DLCV/CN_c7.png)

# CNN Architecture
## AlexNet

![](../img/Learning/DLCV/CA_c1.png)

* Output channels $=$ number of filters $=$ 64
* Output size $W_{out}=(W_{in}-K+2P)/S+1=56$
* Memory that output feature consume
    * Number of output elements $=C_{out}\times H_{out}\times W_{out}=200704$
    * Bytes per element $=4$ (for 32-bit floating point)
    * KB $=$ (number of elements)$\times$ (bytes per element)/1024=784 
* Number of learnable parameters
    * Weight shape $=C_{out}\times C_{in}\times K \times K$
    * Bias shape $=C_{out}=64$
    * Number of parameter $=$ weight $+$ bias $=$ 23296

![](../img/Learning/DLCV/CA_3.png)

* Flatten output size $=C_{in}\times H\times W$
* FCparams $=C_{in}\times C_{out}+C_{out}$
* FC flops $=C_{in}\times C_{out}$

![](../img/Learning/DLCV/CA_c2.png)

## VGG

![](../img/Learning/DLCV/CA_c3.png)

* By stacking 3 by 3 conv, we throw away kernal size as a hyperparam and only need to thing about how many 3x3 conv do we need.
* We can also arbitaryly insert ReLU between these 3x3 conv, allowing more nonlinear computation.

![](../img/Learning/DLCV/CA_c4.png)

## GoogLeNet
* Many innovation for efficiency: reduce parameter count, memory usage, and computation.

![](../img/Learning/DLCV/CA_c5.png)

## Residual Network

When training deeper model, we found that deeper model does worse than shallow model. The initial guess is that Deep model is **overfitting** since it is much bigger than the other model. 

![](../img/Learning/DLCV/CA_c6.png)

## Other

![](../img/Learning/DLCV/CA_c7.png)