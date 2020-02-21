# Data Science: minimum cross-entropy thresholding

## Description
Minimum cross-entropy thresholding or [Li's thresholding](https://www.sciencedirect.com/science/article/abs/pii/003132039390115D)
is a computer vision technique used to binarize images. 
As shown it the following images provided by scikit, this method works relatively well. 

![img](https://scikit-image.org/docs/dev/_images/sphx_glr_plot_threshold_li_001.png)

These results are really good if you consider the fact that this method only provides one single threshold !


## The idea behind it
Minimum cross-entropy thresholding aims to find the threshold at which the information loss due to binarization is the smallest.
The Kullback-Leibler distance (now well known as a standard loss for Variational Auto Encoders) is the starting point of the work of Li et al.
This divergence measures the difference between two distributions.

$$
D(P|Q)= \sum^n_{i=1}p_i\log\left( \frac{p_i}{q_i}\right )
$$

Their contribution is to say that, in order to find the best threshold it is necessary to minimize the cross-entropy between the foreground mean and the foreground, and between the background mean and the background, in mathematical terms:

$$
T_{opt} = argmin\left (  \sum^T_{g=0} gp(g) \frac{g}{\mu_F(T)} +\sum^T_{g=T+1} gp(g) \frac{g}{\mu_B(T)}\right )

\\
\mu_F(T) \text{~is the mean of the foreground at threshold T }
\\
\mu_B(T) \text{~is the mean of the background at threshold T}
\\
g \text{~is the luminance}.
$$

## Implementation
This method is implemented in [scikit.image](https://scikit-image.org/docs/dev/auto_examples/developers/plot_threshold_li.html#sphx-glr-auto-examples-developers-plot-threshold-li-py).
The link gives a lot of good detail about the implementation.
It uses gradient descent to find the optimal threshold.

## Other uses
This method can be used to separate any sample of values as backgound and foreground.
Let's imagine you are running a music service and you would like to find what are the favorite bands of all your users.
You cannot enforce a maximum number of favorite bands, we all have a different amount of bands we adore.
So ranking and picking the top 10 is out of the question.

What you can do is: 
 1. get the count of listened songs per band for every user
 2. apply per user the minimum cross entropy thresholding on the distribution of counts of listened songs per band
 3. filter the bands that have a count of listened songs above the threshold returned by Li's thresholding.
 
The resulting bands are part the "foreground" of this user, therefore you can assume they are the favourite bands.
 
It might be a strong assumption, but I have used Li's thresholding for similar uses, but in different context and it works pretty well !
