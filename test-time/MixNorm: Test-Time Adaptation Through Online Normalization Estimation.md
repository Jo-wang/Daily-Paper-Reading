## [MixNorm: Test-Time Adaptation Through Online Normalization Estimation](https://arxiv.org/abs/2110.11478)

### Introduction and background
- xxx
- xxx
- xxx

### Method
<img width=600 alt="1685345345232" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/02488880-db76-4069-b1b5-c0665ac2b465">

- 1. Replace the BN layer with MixNorm layer.

<img width=600 alt="1685345878649" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ab6d1f56-fcff-4034-94fd-86bc7a969e78">

- 2. initial MixNorm statistics by source statistics. 

  - $\mu^0=\mu^{\text {training }}$ 

  - $\sigma^0=\sigma^{\text {training }}$

- 3. they will be slowly updated by the statistics on each new sample:
  - $\mu^{t+1}=(1-\tau) \mu^t+\tau \mu$

- 4. calculate the local statistics for both org feature $F$ and augmented version $F^{'}$: 
  - <img width=450 alt="1685346646498" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f7d553c1-c7b1-4715-b183-895dc4e1d05b">

- 5. <img width=600 alt="1685346799580" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f73fe8e5-3d68-40c4-9052-ecedfbc536f9">

<img width=600 alt="1685346872798" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a9ae3a7c-bf10-4268-bb07-8e563e873fd2">

### Experiments
- TTA: CIFAR10-C, ImageNet-C
- SFDA: SVHN $\rightarrow$ MNIST, MNIST-M, USPS
- Zero-shot image classification: CIFAR-10/100, STL-10, Stanford Cars, Food101

### Notes
Enables performance for single batch.
