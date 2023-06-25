## [CAFA: Class-Aware Feature Alignment for Test-Time Adaptation](https://arxiv.org/pdf/2206.00205.pdf)


### Introduction and background
- Most adaptation methods require access to the source data during adaptation or modiﬁcation of the training procedure, limiting their applicability.
- A model does not have a chance to learn the test data in a class-discriminative manner since a supervised loss is not available on both the source and target data.
### Method
<img width=700 alt="1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bc990aa9-617c-4960-badd-8b09298c836e">

- Intra-class alignment: align the data with predicted labels in the test set and aim to minimize this.
- Inter-class alignment: we aim to enlarge the distance between the data $x$ and its non-predicted classes.
- We only update the BN.
- We only need a small amount of source data to be used to compute the source per-class statistics.
### Experiments

### Notes
