# Deep Learning for Computer Vision
## Image Classifier - Nearest Neighbor Classifier
Compare a new image with each image in training set using some similarity function. Assign the new image a label as same as the most similar image in training set.

![](../img/Learning/DLCV/NNC_c1.png)

* Using more neighbors helps reduce the effect of outliers.
* When $K > 1$ there can be ties between classes, which needed to be break somehow.

![](../img/Learning/DLCV/NNC_c2.png)

* The idea #2 is bad because when we adjust the hyperparameters according to the test set, we pollute it and it has little differences with training set.
* Remember that test set can be used only once in the final test.

![](../img/Learning/DLCV/NNC_c3.png)


If we want to have a good prediction on a new image, we need a large amount of examples on training set, which grows exponentially with dimension.

![](../img/Learning/DLCV/NNC_c4.png)

## Linear Classifier

![](../img/Learning/DLCV/LC_c1.png)

Bias Trick is less common to use in practice because when we separate the weight and the bias into separate parameters, we can treat them differently on how they are initialized or regularized.

![](../img/Learning/DLCV/LC_4.png)

![](../img/Learning/DLCV/LC_5.png) 

We can visualize the "template" for each category

![](../img/Learning/DLCV/LC_6.png) 

![](../img/Learning/DLCV/LC_7.png) 

The score goes linearly with respect to the change of pixels. We can extend this to high dimensions. The changes of scores are consistent with those hyperplanes. 

![](../img/Learning/DLCV/LC_8.png) 

![](../img/Learning/DLCV/LC_9.png) 

This also account for why perceptron, actually a linear classifier, couldn't learn XOR.

Now we can compute class scores for an image with given $W$. To get a good $W$, we need to do:

* Use a **loss function** to quantiy how good a value of $W$ is.

* Find a $W$ that minimizes the loss function.

![](../img/Learning/DLCV/LC_c2.png) 

Different regularization functions give the model extra hints about what types of classifier we'd like them to learn.

For example, L2 regularization likes to spread out the weight while L1 regularization does in the opposite way.

![](../img/Learning/DLCV/LC_c3.png) 

It's important to notice the loss function on random values, if your model get a worse loss value after training, there must be sth bad.

![](../img/Learning/DLCV/LC_18.png) 

![](../img/Learning/DLCV/LC_19.png) 

SVM Loss is easy to get to zero point while Cross-Entropy nearly impossible to get to zero.

## Optimization

* goal: find $w^{*}=argmin_{w}L(w)$

![](../img/Learning/DLCV/Op_1.png)

![](../img/Learning/DLCV/Op_2.png)

How to evaluate gradient?

* Numeric gradient
    * We can approximate the gradient by defination. Increasing one slot of the weight matrix by a small step and recompute loss function. Use the defination of derivative to get a approximation of gradient.
    * Takes lots of time and not accurate.


![](../img/Learning/DLCV/Op_3.png)

* Analytic gradient
    * exact, fast, error-prone

![](../img/Learning/DLCV/Op_4.png)

* In practice, always use analytic gradient, but check implementation with numerical gradienet. This is called a ***gradient check***

### Gradient Descent

![](../img/Learning/DLCV/Op_5.png)

### Stochastic Gradient Descend

* We don't use the full training data but some small subsamples of it  to approximate loss function and gradient, for computing on the whole set is expansive. These small subsamples are called ***minibatches***

![](../img/Learning/DLCV/Op_c1.png)

* SGD + Momentum may overshoot in the bottom for its historical speed and will come back.

![](../img/Learning/DLCV/Op_13.png)

* Progress along "steep" direction is damped. Progress along "flat" directions is accelerated.

* The learning rate will continuely decay since `grad_squared` gets larger and larger.

![](../img/Learning/DLCV/Op_14.png)

![](../img/Learning/DLCV/Op_15.png)

* We initialize `moment2` as 0 and if we take `beta2` closely to 0, the `moment2` will also close to 0, which may make our first gradient step very large. This could cause bad results.

![](../img/Learning/DLCV/Op_c2.png)

* Second-order optimization is better to use in low dimension. 

![](../img/Learning/DLCV/Op_20.png)

## Neural Network
To solve the limitation of linear classifier, we can apply feature transformation.

![](../img/Learning/DLCV/NN_c1.png)

### Activation function

![](../img/Learning/DLCV/NN_4.png)

![](../img/Learning/DLCV/NN_5.png)

### Neuron
![](../img/Learning/DLCV/NN_6.png)

### Space Warping

![](../img/Learning/DLCV/NN_SW.png)

The more the layer, the more complex the model is. Try to adjust regularization parameter to solve it.

![](../img/Learning/DLCV/NN_size_reg.png)

### Universal Approximation
A two layer neural network can approximate any function. But it may need a large size to get high fidelity.

![](../img/Learning/DLCV/NN_UA.png)


### Convex Functions
Taking any two points in the input, the secant line will always lie above the function between that two points.

![](../img/Learning/DLCV/NN_convex.png)

However, most neural networks need **nonconvex optimization**

## Backpropagation

![](../img/Learning/DLCV/BP_c1.png)

### Computation Graph

![](../img/Learning/DLCV/BP_c2.png)

### Backprop Implementation

![](../img/Learning/DLCV/BP_c3.png)

* You can define your own node object in computation graph using pytorch API

### Backprop with Vectors

![](../img/Learning/DLCV/BP_c4.png)

### Backprop with Matrics

* $dL/dx$ must have the same shape as $x$ since loss $L$ is a scalar

![](../img/Learning/DLCV/BP_c5.png)

Assume we want to derive $dL/dx_{i,j}$

* Note that only the $ith$ row of $y$ is formed by $x_{i,j}$ and corresponding coefficients are the $jth$ row of $w$.
* So $dL/dx_{i,j}$ is just the inner product of the $ith$ row of $dL/dy$ and the $jth$ column of $w^{T}$, which leads to the result of $dL/dx=(dL/dy)w^{T}$

![](../img/Learning/DLCV/BP_c6.png)

### High-Order Derivatives
$\frac{\partial ^{2}L}{\partial x_{0}^{2}}$ is $D_{0} \times D_{0}$ dimension for it's the derivative of $\frac{\partial L}{\partial x_{0}}$, which is a $D_{0}$ dimension vector.

![](../img/Learning/DLCV/BP_c7.png)