## [Improved Test-time Adaptation for Domain Generalization](https://arxiv.org/abs/2304.04494)

CVPR2023

### Introduction and background
- Selecting an appropriate auxiliary TTT task is crucial, and an inappropriate one that does not align with the main loss may deteriorate instead of improve the performance.
- Identifying reliable parameters to update is also essential for generalization
- To solve the above two issues, this paper proposes two parts.
### Method
#### Learnable consistency loss for TTT
- <img width=300 alt="a23" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e2682090-89ec-4c1c-995f-c80f07a587de">      


- <img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/fe39fe18-4cb4-41db-87bf-d8b9a93b05b7">

- <img width=380 alt="a2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7e04f369-125a-4e28-9179-81fd05b1de68">

where the third line from the bottom of the algorithm is to align the directions between the main task (considers both the original prediction and the augmented one) and the aux task from the gradient perspective, as the right figure shows. The augmented feature is obtained by modifying the intermediate activation in $f_\theta (x)$.

#### Additional Adaptive Parameters
- <img width=400 alt="awwre" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d8c5d14b-4f0e-4cff-ae79-157349a3381f">

- Original methods mainly update the BN parameter or encoder/classifier. This paper proposes to insert a block for each conv block in the feature extractor and aims only to update the parameters in the newly inserted blocks.
- From $z^i=f_\theta^i\left(z^{i-1}\right)$, s.t. $z^1=f_\theta^1(x)$
- To $z^i=f_{\Theta}^i\left(f_\theta^i\left(z^{i-1}\right)\right)$, s.t. $z^1=f_{\Theta}^1\left(f_\theta^1(x)\right)$
  where $\Theta$ is the parameters for newly inserted blocks. $i-1$ means the previous original block.
  
### Experiments
- ResNet-18
- PACS, VLCS, DomainNet, OfficeHome, TerraInc
- Single source/multi-source

### Notes
Out of Online TTA scope. Not share any same dataset.
