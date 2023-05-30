## [Revisiting realistic test-time training: Sequential inference and adaptation by anchored clustering](https://arxiv.org/abs/2206.02721)

https://github.com/Gorilla-Lab-SCUT/TTAC

NeurIPS2022

### Introduction and background
- The background of the paper is the problem of adaptation in test-time training (TTT) when deploying models on target domain data subject to distribution shift. 
- The authors note that access to full source domain data is often not available, and instant inference on target domain is required. 
- The motivation for this paper is to propose a realistic sequential protocol for adaptation in TTT and introduce a novel approach called test-time anchored clustering (TTAC) to enable efficient inference on target domain data. 
- The authors aim to address the confusion over experimental settings in TTT, which has led to unfair comparisons between different approaches. 
- They categorize TTT protocols by two key factors and demonstrate that TTAC consistently outperforms state-of-the-art methods on six TTT datasets. 
- The paper also provides more details on the derivation of iterative updating target domain cluster parameters, hyperparameters used in TTAC, evaluation of TTAC with transformer backbone, ViT, additional evaluation of TTAC update epochs, the stability of TTAC under different data streaming orders, and compared alternative target clustering updating strategies.

### Method
- Previous TTT (Test-time Training) has two confusion: 
  - whether training objective must be modified
  - whether sequential inference on target domain data is possible
- **This paper neither modifies the training objective nor violates sequential inference**

#### Anchored Clustering for Test-Time Training
- Assume source and target distribution are mixture of gaussians.
 
  <img width=300 alt="1685419985771" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/92fd4d6b-4da0-41a8-a762-866f7a6eba21">
- allocate the same number of clusters in both source and target domains and each target cluster is assigned to one source cluster

- Min the KL between source class and its corresponding target class

  <img width=450 alt="1685421143363" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b13fbda2-d511-4169-8aa6-ac6aac78dc35">

#### Clustering through Pseudo Labeling
- Given the predicted pseudo labels, we could estimate the mean and covariance for each component Gaussian with the pseudo labeled testing samples. But pseudo label has confirmation bias.
- To reduce the impact of incorrect pseudo labels, use temporal consistency (TC) pseudo label filtering.
- calculate the temporal exponential moving averaging posteriors:

  <img width=600 alt="1685427293098" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bc1c5b46-8ab0-410b-aa15-0ccee3b38605">

#### Global Feature Alignment
- since we filter out so much "unreliable" pseudo labels, the target class distribution may not accurate, so we min the KL between source and target distribution:
  <img width=600 alt="1685428385700" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a9ec44a8-c221-4cc9-a74f-4948dbcc7951">

#### Efficient Iterative Updating
<img width=600 alt="1685428471768" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4369b5d1-8631-4c17-a26d-f06f72b6bcde">

<img width=600 alt="1685428487146" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e1ae7c70-c4ad-436f-8a8a-4ea5eb80113f">

<img width=600 alt="1685447583021" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bb5643cd-8435-41e9-b4b4-a4dedcefc4b3">

### Experiments
- Dataset: CIFAR10C/100C; ImageNet-C; VISDA-C; CIFAR10.1; ModelNet40-C
### Notes
