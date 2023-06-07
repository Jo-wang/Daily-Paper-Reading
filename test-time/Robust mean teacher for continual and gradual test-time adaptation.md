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

#### Source Replay

### Experiments

### Notes
