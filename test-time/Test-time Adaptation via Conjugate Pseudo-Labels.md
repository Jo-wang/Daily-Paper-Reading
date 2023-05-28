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
  - **Observation 1:** for the classifier trained with CE, the meta-TTA loss is temperature-scaled softmax entropy.
  - **Observation 2:** for a classifier trained with squared loss, the meta-TTA loss is a negative squared loss.
  - The best TTA loss is depends on the loss used to train the source classifier.
- Conjugate Pseudo label:
  <img width=600 alt="Screen Shot 2023-05-28 at 13 30 42" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f991a803-d978-4599-9e0c-ce767db98a5f">
  where f is the logsumexp operation when the source model is trained by the CE loss.

### Experiments
![1685317764983](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a349b392-8a36-4886-a2cc-d39493fc174c)
![1685317779120](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/19ee86bd-b621-45e3-b8e0-17109712c3cb)
![1685317793947](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/fffa5219-e2bc-4fb1-ba7c-126d7bd77a85)

### Notes
