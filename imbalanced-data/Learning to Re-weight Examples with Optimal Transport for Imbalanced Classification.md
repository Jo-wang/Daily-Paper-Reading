## [Learning to Re-weight Examples with Optimal Transport for Imbalanced Classification](https://arxiv.org/pdf/2208.02951.pdf)
NeurIPS 2022

### Introduction and background
- Most real-world datasets are imbalanced, training model would be signiﬁcantly dominated by those majority classes
- The major challenge of imbalanced classification is essentially the mismatch between the imbalanced training dataset and the balanced test set.
- Previous methods of dealing with imbalanced data is re-weighting (in loss functions), including re-sampling, class-level or instance-level re-weighting, meta-learning, two-stage methods and post-hoc correction.
- L2RW set the weight as a learnable parameter with unbiased meta set, but the parameter is coupled with the to-be-learned classifier. The dependence of weights on classiﬁer at training stage may lead to inaccurate learning of the weights.

### Method
- Math:  
$D_{train}$: imbalanced training data  
$D_{meta}$: small balanced meta set
$f(x, \theta)$: model, parameterized by $\theta$

- 

### Experiments

### Notes
