## [Robust mean teacher for continual and gradual test-time adaptation](https://arxiv.org/abs/2211.13081)

CVPR2023

Ranking: 1 - 5, 5 means very important
### Introduction and background
- the effectiveness of most TTA methods is only demonstrated for a single domain shift at a time

### Method
<img width=400 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7e8a1550-c191-4c10-8fc1-3d44e3a16d7d">

#### Robust Mean Teacher
- Instead of using CE for mean teacher, this paper prove that symmetric CE is better. So the KD loss is:

  <img width=300 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d4fa1137-b892-407d-86b9-608d9170c92c">
  
  where teacher is $q_t^{\mathrm{T}}$ student is $p_t^{\mathrm{T}}$, current test data is $x_t^{\mathrm{T}}$ and $\tilde{x}_t^{\mathrm{T}}=\text{Aug}(x_t^{\mathrm{T}})$

- Mean teacher warm-up for more accurate predictions: Warm-up is conducted offline with the same batch size used during test time by minimizing $\mathcal{L}_{\mathrm{SCE}}$ for one epoch on 50, 000 source training samples. Note that no augmentation is applied during warm-up.

#### Contrastive Learning
- Get source prototype for each class c by averaging $r_c^{\mathrm{S}}$
- For each test sample $i$, get the closest source prototype and agumented view.
- Use contrastive loss for source/test/augmented test samples:
- For each sample $i$, we have a closest source prototype and a augmented view. So the total sample number is $3\cdot N$

  <img width=300 alt="img" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cb501b88-ffee-42a6-926e-a43412041f1a">
  
  where $i$ is $i \in I:=\{1, \ldots, 3 N\}$, and $z$ is the output of the non-linear projection of input samples' feature. $z_v$ is test sample augmented view feature. $z_a$ is any other sample feature exclude $i$.
  
#### Source Replay
- **Part of source data can be saved in a buffer**, then use CE loss to replay these data to update the model parameter.

### Experiments
- Dataset: CIFAR10C/100C; ImageNet-C; ImageNet-R; DomainNet-126
- Continual online TTA

<img width=700 alt="img1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f35d7c7a-6ce5-481e-bdf6-331af60d804d">

- See paper for exp of gradual TTA.
### Notes
