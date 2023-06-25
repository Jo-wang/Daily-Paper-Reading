## [CAFA: Class-Aware Feature Alignment for Test-Time Adaptation](https://arxiv.org/pdf/2206.00205.pdf)


### Introduction and background
- Most adaptation methods require access to the source data during adaptation or modiﬁcation of the training procedure, limiting their applicability.
- A model does not have a chance to learn the test data in a class-discriminative manner since a supervised loss is not available on both the source and target data.
### Method
<img width=700 alt="1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bc990aa9-617c-4960-badd-8b09298c836e">
<img width=700 alt="11" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5656f85b-b362-46aa-b96c-cb21c6f8f43b">

- Pre-compute source statistics:

  <img width=400 alt="11df" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/691b7506-0890-4e31-9093-19c2e3877e2a">
        
- Define the distance between two distributions as the Mahalanobis distance (input image $x$, feature extractor $g(\cdot)$, Gaussian distribution $\mathcal{N}$): $D(x ; \boldsymbol{\mu}, \boldsymbol{\Sigma})=(g(x)-\boldsymbol{\mu})^{\top} \boldsymbol{\Sigma}^{-1}(g(x)-\boldsymbol{\mu})$
  
- Intra-class alignment: align the data with predicted labels in the test set and aim to minimize this $D_{\text{intra}}(x_t, y_t)=D(x_t; \mu_{y_t}, \Sigma_{y_t})$:

  <img width=250 alt="1j1df" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b9cf09be-a0a6-4dec-a5ad-ec818b224b72">

  where $N$ is the number of image samples.
  
- Inter-class alignment: we aim to enlarge the distance between the data $x$ and its non-predicted classes.
  
  <img width=250 alt="1jk1df" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/c10c0177-b35d-46ce-9482-5759bd5f888b">

- The final loss function could be:
  
  <img width=250 alt="1jkm1df" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8f492957-43a2-467c-914f-a83200fcf93d">

- We only update the BN.
- We only need a small amount of source data to be used to compute the source per-class statistics.
### Experiments
- Dataset: CIFAR-10C/100C; ImageNet-C; TinyImageNet-C; OfficeHome; DomainNet
- backbone: R-50

### Notes
