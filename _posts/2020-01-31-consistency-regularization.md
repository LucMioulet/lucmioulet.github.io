# Consistency regularization

## The issue with data augmentation
Data augmentation has become central to training most deep learning models as data is the key.
The idea behind data augmentation is that by being trained on many slightly distorted instances of a labeled data point, the model will learn to create a smoother decision boundary.

Data-augmentation, dropout, model-selection, stochastic gradient descent all introduce parts of randomness in the training process of a model.
This means that the same data-point and its data augmented set might provide different labels.
This inconsistenty of the model output might be acceptable during the training regime of a model, but not during the inference.

## Consistency regularization
Consistency regularization is a Semi-Supervised technique that, turns the issue of having this output inconsitency into an advantage.
A new loss $$ L_{cons} $$ is added to the training loss. The $$ L_{cons} $$ loss is in charge of minimizing the distance between the different outputs produced from an augmented input.

$$ 
L_{cons} =  d(f_\theta(x), f_\theta(\hat{x}))
$$

Any distance could be used, euclidean, cross-entropy, etc... it depends on the output type received.

Forcing this consistency forces the model smoothes the decision boundaries.
The article [1](https://arxiv.org/pdf/1906.01916.pdf) makes a pretty good illustation, of this phenomenon.
![Boundaries](images/consistency-regularization-decision-boundary.png)

By using few supervised labels a model would only learn a very rough boundary decision. 
With consistency regularization it can learn to produce a smoother boundary decision on the labeled data, the unlabeled data helps expand the decision boundary to areas with very few labels (low density regions). 

## Application
**Consistency regularization means that you could train a classification model, using unlabeled data for which the models task is produce a consistent output for input variation !**

This has been applied to GANs for example. The Discriminator is fed perturbed versions of an output of the Generator and is trained to maintain consistency. 
This avoids to have an hyper sensitive discriminator that would react to very precise generator artifacts.
A discriminator with smoother bounds will enable the GAN to train for longer and avoids having a generator that discover this one trick to dupe the discriminator. At least in principle
  
## Next  
I am working on a notebook to test this idea. To be followed !

## Sources

[Constitency regularization for GANs](https://deepai.org/publication/consistency-regularization-for-generative-adversarial-networks)
[Semi-supervised semantic segmentation needs strong,high-dimensional perturbations](https://arxiv.org/pdf/1906.01916.pdf)
[Regularization With Stochastic Transformations andPerturbations for Deep Semi-Supervised Learning](https://arxiv.org/pdf/1606.04586.pdf)
