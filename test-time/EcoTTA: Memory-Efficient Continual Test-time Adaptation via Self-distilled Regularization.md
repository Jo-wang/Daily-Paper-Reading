## [EcoTTA: Memory-Efficient Continual Test-time Adaptation via Self-distilled Regularization](https://arxiv.org/abs/2212.09713)

CVPR2023

### Introduction and background
- xxx
- xxx
- xxx

### Method

<img width=700 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e4f37a0d-d335-4b29-b7e2-ae53d1e64260">

#### Source pretraining
- Pretrain the source model in a simple supervised manner
- Freeze original pretrained model, Split the encoder of the pretrained model into K parts, for each part, insert a **meta network** consists of a BN and a Conv block (Conv + Bn + ReLU)
- Warm up the meta network for a small amount of epochs (10 epochs for CIFAR)

#### TTA

### Experiments

### Notes
