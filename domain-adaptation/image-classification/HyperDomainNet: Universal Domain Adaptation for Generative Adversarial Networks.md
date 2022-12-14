## [HyperDomainNet: Universal Domain Adaptation for Generative Adversarial Networks](https://arxiv.org/abs/2210.08884)
NeurIPS2022

Ranking: 3.8
### Introduction and background
- The standard approach of GAN TL methods is to fine-tune almost all weights of the pretrained model. (reasonable if target domain is very far from the source one)
- there is a wide range of cases when the distance between data domains is not so far (no need to fine-tune all weights of the source generator)
- **propose a novel domain-modulation operation that reduces the parameter space for fine-tuning the StyleGAN2 (to optimize for each target domain only a single vector d. We incorporate this vector into the StyleGAN2 architecture through the modulation operation at each convolution layer. )**
- conventional multi-source train separate generators
- **this paper propose to train a hyper-network that predicts the vector d for the StyleGAN2 depending on the target domain.**

### Method
![1671060513852](https://user-images.githubusercontent.com/46414159/207737343-242059f6-2ea8-43c0-9dc1-b6f643bb2fd1.png)

### Experiments

### Notes
