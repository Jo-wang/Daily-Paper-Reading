## [Cycle Self-Training for Domain Adaptation](https://arxiv.org/abs/2103.03571)
NeurIPS 2021

Ranking: 4.5
### Introduction and background
1. Self-training with pseudo labeling is a replacement of original feature alignment in domain adaptation.
2. Pseudo-labels are unreliable:
    -  pseudo-labels are biased towards several classes due to domain shift
    -  the denoising ability of pseudo-labels in standard self-training is hindered by domain shift

### Method
![Screen Shot 2022-11-07 at 16 19 10](https://user-images.githubusercontent.com/46414159/200239162-01979919-4579-47ac-a188-cfe5760eeba6.png)

Source distribution $P$, target distribution $Q$, model $f$ has feature extractor $h_{\phi}$ and a head (linear classifier) $g_{\theta}$.
#### Cycle Self-training
- Forward Step: source classifier $\theta _{s}$ trained on top of the shared representation $\phi$ , and then use it to generate target pesudo-labels:
![Screen Shot 2022-11-07 at 17 28 24](https://user-images.githubusercontent.com/46414159/200250768-5cac86f5-4671-463b-b00f-e4aa2f83b816.png)

- Reverse Step
- Bi-level Optimization

#### Tsallis Entropy Minimization

### Experiments

### Notes

