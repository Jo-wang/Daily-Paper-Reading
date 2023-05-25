## [Test-Time Classifier Adjustment Module for Model-Agnostic Domain Generalization](https://openreview.net/forum?id=e_yvNqkJKAW)

NeurIPS2021

### Introduction and background
- **Background:**
Deep neural networks have achieved remarkable success in various machine learning tasks, but they often suffer from poor generalization performance when the test data comes from a different distribution than the training data. This is known as the domain shift problem, and it can significantly affect the accuracy and reliability of machine learning models in real-world scenarios.

- **Motivations:**
The main motivation of this paper is to address the domain shift problem in deep neural networks by proposing a new method for model-agnostic domain generalization. 

  Specifically, the proposed Test-Time Classifier Adjustment Module for Model-Agnostic Domain Generalization (T3A) aims to make machine learning models more robust to unknown distribution shifts during test time by correcting predictions during test phase, rather than just training phase.

  The authors also aim to demonstrate that T3A is computationally efficient, applicable to different types of deep neural networks, and can be used together with existing DG algorithms.

  Overall, this paper seeks to improve the generalization performance of deep neural networks in real-world scenarios where the test data may come from a different distribution than the training data.

### Method T3A
1. Train a deep neural network on multiple source domains.
2. At test-time, use T3A to adjust the weights of the linear classifier (the last layer of deep neural networks).
3. Create a pseudo-prototype for each class using online unlabeled data and the classifier trained in the source domains.
4. Classify each sample based on its distance to the pseudo-prototype.
5. The adjusted decision boundary avoids the high-data density region on the target domain and reduces the ambiguity (entropy) of predictions, which is known to be connected to classification error.
6. Since T3A does not alter the training phase, it can be used together with existing DG algorithms.
### Experiments

### Notes
