## [Test-time Adaptation via Conjugate Pseudo-Labels](https://arxiv.org/pdf/2207.09640.pdf)

NeurIPS2022

### Introduction and background
 
The background of this paper is the problem of distribution shift in machine learning, which occurs when the distribution of the test data differs from that of the training data. 

This can lead to a decrease in performance of machine learning models, as they may not generalize well to new data. 

Test-time adaptation (TTA) is a technique that aims to address this problem by adapting neural networks to distribution shifts with access to only unlabeled test samples from the new domain at test-time.

The motivation for this paper is to explore and improve TTA methods, which have gained interest in recent years. The authors note that it can be difficult or even impossible to precisely characterize all possible distribution shifts a model could encounter and then train accordingly. 

Instead, they propose a method called Conjugate Pseudo-labels for TTA, which involves updating the source model parameters via a few steps of optimization on an unsupervised objective involving the new test sample from the target distribution. 

The authors aim to demonstrate that their method outperforms existing TTA methods on several benchmark datasets and provide insights into how TTA can be improved in practice.

### Method
- This paper want to use meta-learning to find out which loss function is suitable for TTA task: 
### Experiments

### Notes
