
## [Test-Time Adaptation via Self-Training with Nearest Neighbor Information](https://openreview.net/forum?id=EzLtB4M1SbM)

ICLR2023 poster

Ranking: :star: :star: :star: :star:

### Introduction and background
- Current TTA fall into 3 categories:
  - norm-based: replaces the batch normalization (BN) statistics of the trained
model with the BN statistics estimated on test data (only update BN parameters)
  - Entropy minimization: fine-tune the trained feature extractor, which is the trained classifier except the last linear layer, by minimizing the prediction entropy of test data;
  - prototype-based: modifies a trained linear classifier (the last layer) by using the pseudo-prototype representations of each class and the prototype-based classification for test data, where the prototypes are constructed by previous test data and the prediction for the data from trained classifier
- xxx

### Method

### Experiments

### Notes
