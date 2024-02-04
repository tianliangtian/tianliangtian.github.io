# Deep Learning for Computer Vision
## Image Classifier
### Nearest Neighbor Classifier
Compare a new image with each image in training set using some similarity function. Assign the new image a label as same as the most similar image in training set.

![](../../img/Learning/DLCV/NNC_1.png)

![](../../img/Learning/DLCV/NNC_2.png)

![](../../img/Learning/DLCV/NNC_3.png)

![](../../img/Learning/DLCV/NNC_4.png)

![](../../img/Learning/DLCV/NNC_5.png)

* Using more neighbors helps reduce the effect of outliers.
* When $K > 1$ there can be ties between classes, which needed to be break somehow.

![](../../img/Learning/DLCV/NNC_6.png)

![](../../img/Learning/DLCV/NNC_7.png)

![](../../img/Learning/DLCV/NNC_8.png)

* The idea #2 is bad because when we adjust the hyperparameters according to the test set, we pollute it and it has little differences with training set.
* Remember that test set can be used only once in the final test.

![](../../img/Learning/DLCV/NNC_9.png)

![](../../img/Learning/DLCV/NNC_10.png)

![](../../img/Learning/DLCV/NNC_11.png)

If we want to have a good prediction on a new image, we need a large amount of examples on training set, which grows exponentially with dimension.

![](../../img/Learning/DLCV/NNC_12.png)

![](../../img/Learning/DLCV/NNC_13.png)

![](../../img/Learning/DLCV/NNC_14.png)

![](../../img/Learning/DLCV/NNC_15.png)

### Linear Classifier

![](../../img/Learning/DLCV/LC_1.png)

![](../../img/Learning/DLCV/LC_2.png)

![](../../img/Learning/DLCV/LC_3.png)

Bias Trick is less common to use in practice because when we separate the weight and the bias into separate parameters, we can treat them differently on how they are initialized or regularized.

![](../../img/Learning/DLCV/LC_4.png)

![](../../img/Learning/DLCV/LC_5.png) 

We can visualize the "template" for each category

![](../../img/Learning/DLCV/LC_6.png) 

![](../../img/Learning/DLCV/LC_7.png) 

The score goes linearly with respect to the change of pixels. We can extend this to high dimensions. The changes of scores are consistent with those hyperplanes. 

![](../../img/Learning/DLCV/LC_8.png) 

![](../../img/Learning/DLCV/LC_9.png) 

This also account for why perceptron, actually a linear classifier, couldn't learn XOR.

Now we can compute class scores for an image with given $W$. To get a good $W$, we need to do:

* Use a **loss function** to quantiy how good a value of $W$ is.

* Find a $W$ that minimizes the loss function.

![](../../img/Learning/DLCV/LC_10.png) 

![](../../img/Learning/DLCV/LC_11.png) 

![](../../img/Learning/DLCV/LC_12.png) 

![](../../img/Learning/DLCV/LC_13.png) 

![](../../img/Learning/DLCV/LC_14.png) 

Different regularization functions give the model extra hints about what types of classifier we'd like them to learn.

For example, L2 regularization likes to spread out the weight while L1 regularization does in the opposite way.

![](../../img/Learning/DLCV/LC_15.png) 

![](../../img/Learning/DLCV/LC_16.png) 

![](../../img/Learning/DLCV/LC_17.png) 

It's important to notice the loss function on random values, if your model get a worse loss value after training, there must be sth bad.

![](../../img/Learning/DLCV/LC_18.png) 

![](../../img/Learning/DLCV/LC_19.png) 

SVM Loss is easy to get to zero point while Cross-Entropy nearly impossible to get to zero.