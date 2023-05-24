## [Domain-agnostic test-time adaptation by prototypical training with auxiliary data](https://openreview.net/pdf?id=bAO-2cGNX_j)

NeurIPS2021

### Introduction and background
- The proposed method, called PAD (Prototypical Training with Auxiliary Data), is motivated by the problem of test-time adaptation (TTA) in machine learning. TTA aims to achieve high accuracy on out-of-distribution (OOD) target data with only model parameters trained on the source domain and the target data. However, standard TTA assumes that the test data is under a single distribution, or the distribution gradually changes with test data streaming in. 

- PAD addresses this limitation by introducing a new problem setting called Domain-agnostic Test-time Adaptation, where only a model trained on source data is available during testing and test data have an unpredictable distribution and can change abruptly. The motivation behind PAD is to perform prototypical training while using auxiliary data to regularize the training process, resulting in consistently superior performance over previous methods on two datasets Mixed CIFAR-10-C (curated from CIFAR-10-C) and CIFAR-10.1. More surprisingly, PAD achieves better test accuracy on OOD distribution (CIFAR-10.1) than the in-domain distribution (CIFAR-10).

- **The task: Domain-agnostic Test-time Adaptation
(DaTTA), in which the source data is unavailable during test time, and the test data distribution is unknown and varies abruptly.**

### Method
<img width=700 alt="image" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/c39f7663-5305-48e5-9602-7c664ad3c10c">
where h is a cosine classifier whose weights can be regarded as the prototypes for each category.

#### Prototypical Learning with Augmented Samples

- Set up the model with one encoder g and one cosine classifier h (cosine classifier is a typical method in prototypical learning so that we can directly treat the weight as prototype of each category)
- During source training, get the prototype by the classifier h.
- For testing, augmentation test sample $x_0$ into multiple augmentations $x_1$ ... $x_n$. Then get the prediction $\hat{y}$ by majority voting.
- minimize the L1 loss between each feature $z_i$ = g($x_i$; $\cdot$) and the prototype p corresponding to $\hat{y}$
- Only compute the loss on $x_0$ if the prediction $\hat{y}_0$ on the original image is consistent with $\hat{y}$ and the number of supporting votes is more than half.
- Loss for one sample: <img width=200 alt="1684892593036" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e8785e61-07b9-4720-9062-0cc49326b9ea">
- The loss over <img width=300 alt="1684892679001" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4708983b-b781-4a77-b9b7-fd7d369f6b71"> is:

 <img width=200 alt="1684892766086" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/db5ad7e5-10dd-4965-91f5-b711c6618224">


#### Auxiliary Data Regularization

Use aux data to suppliment the main task: we have two feature extractor, the $g(\cdot ; \theta)$ will be updated during TTA and $g(\cdot ; \theta_0)$ is fixed source version.
- input aux data to get $z$ and $z_0$, let $Z^l$ and $Z^{l,0}$ be the activations of l-th layer from $g(\cdot ; \theta)$ and $g(\cdot ; \theta_0)$.
- Calculate <img width=200 alt="1684894712846" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a392694a-0877-4bd2-ab89-f1b4a8c877e0">
- Compute loss <img width=200 alt="1684894752216" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8a42bd7f-cfb5-4f50-a28e-f8fcf7057980">

where $\|\cdot\|_F$ is the Frobenius norm. this is the $\mathcal{L}_{\text {aux }}$.


#### PAD Learning

<img width=200 alt="1684894917044" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e592f206-dccc-46a0-a12e-76c21b3e2474">


### Experiments
- CIFAR10-C CIFAR10.1 batch size is 1. Aux data is Tiny-Imagenet-200.
![1684895278159](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/710b6e50-b02b-47bf-8356-2d0661e53fd9)

### Notes
No backbone specified. No code available.
