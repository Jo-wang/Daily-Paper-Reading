## [Covariance-aware Feature Alignment with Pre-computed Source Statistics for Test-time Adaptation](https://arxiv.org/pdf/2204.13263.pdf)

### Introduction and background
- Adapting BN layers works well on uniform distribution shifts, such as a single type of image corruption (e.g., noise or blur), but fails to adapt to complex distribution shifts, such as mixed types of image corruption.
- Prior TTA methods other than those that adapt BN layers perform poorly on such complex distribution shifts
- The target mini-batch covariance matrix degenerates as a result of the **batch size being smaller than the number of feature dimensions**

### Method
<img width=500 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3f0fca23-8f58-4f82-b55f-98d5ed1cdb04">

<img width=600 alt="adgfew" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2f0a21af-6fdc-4b88-aaf6-ce38db0ccad0">

<img width=600 alt="agreg" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5c8d142d-ddce-4384-9b6e-84211964d31e">

#### Pre-computing the Statistics
<img width=700 alt="dwa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d672eeb4-6e24-428c-b0fa-b73f976b9235">

#### TTA for feature alignment
We compute the feature alignment loss by the JS divergence between source and target (batch level) statistics: <img width=300 alt="adew" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f6b83a3e-b3a5-4d50-a8dc-d34ffda2df48">

However, according to the cluster assumption: natural data form clusters and decision boundaries should lie in low-density regions. The actual feature representations may form clusters such as classes. So we further use infomax loss: <img width=300 alt="dfewf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e96e7675-306a-4f92-a0ed-ea63db166a02">

<img width=700 alt="dfecwf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4fda6bf7-792d-4e64-ab91-4037e6204352">


#### Feature Grouping
The target covariance matrix $\Sigma$ calculated over a mini-batch will degenerate and det($\Sigma^t$) become zero since the number of dimensions (e.g., 2,048 in the case of ResNet-50) is larger than the ordinary batch size. 

Before computing $\mathcal{L}_a$, we perform feature grouping to break down the dimensions of the feature representations {1; ; ; ;d} into groups smaller than the batch size and then compute the feature alignment loss for each group.

<img width=700 alt="dfefcwf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/59568a88-485a-46e1-8eaa-7595eed981aa">

<img width=700 alt="dfewcwf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/07c41847-31c7-4d72-aa55-35b5cbe03d06">

The highlighted green part looks not correct.

### Experiments
- CIFAR10C/100C; ImageNet-C/R
- R-26, R-50
- BS=256
- k=128
    
<img width=600 alt="agrhheg" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a3929319-1f05-4a8a-a224-4bbfb15db1d2">
    
<img width=600 alt="agreeeg" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/993546d4-ca19-4693-a562-853d71562c8c">

### Notes
