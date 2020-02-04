# Consistency regularization


Data augmentation has become central to training most deep learning models as data is the key.
The idea behind data augmentation is that by being trained on many slightly distorted instances of a labeled data point, the model will learn to create a smoother decision boundary.

Data-augmentation, dropout, model-selection, stochastic gradient descent all introduce parts of randomness in the training process of a model.
This means that the same data-point and its data augmented set might provide different labels.
This inconsistenty of the model output might be acceptable during the training regime of a model, but not during the inference.

Consistency regularization is a Semi-Supervised technique that, turns the issue of having this output inconsitency into an advantage.


## Sources

[Data Augmentation]()
[](https://deepai.org/publication/consistency-regularization-for-generative-adversarial-networks)
[Semi-supervised semantic segmentation needs strong,high-dimensional perturbations](https://arxiv.org/pdf/1906.01916.pdf)
[Regularization With Stochastic Transformations andPerturbations for Deep Semi-Supervised Learning](https://arxiv.org/pdf/1606.04586.pdf)
