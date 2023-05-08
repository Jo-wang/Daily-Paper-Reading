## [A Comprehensive Survey on Test-Time Adaptation under Distribution Shifts](https://arxiv.org/pdf/2303.15361.pdf)

### Introduction
- Test-time domain adaptation (source-free domain adaptation): utilizes all test batches for multi-epoch adaptation before generating final predictions.
- Test-time batch adaptation (TTBA): individually adapts the pre-trained model to one or a few instances.
- Online test-time adaptation (OTTA): adapts the pre-trained model to the target data {b1, · · · , bm} in an
online manner, where each mini-batch can only be observed
once.
- Test-time prior adaptation (TTPA): label shift scenario within the TTA framework

### Related work
- Domain adaptation & Domain generalization
- Hypothesis Transfer Learning
- Continual Learning and Meta-Learning
- Data-Free Knowledge Distillation
- Self-Supervised and Semi-Supervised Learning
- Test-Time Augmentation

### Method
#### SFDA
<img width=400 alt="1683509941416" src="https://user-images.githubusercontent.com/46414159/236715575-268b5eaa-5174-446f-bb8e-3f78d1116a08.png">

#### TTBA
![1683531215912](https://user-images.githubusercontent.com/46414159/236763425-c5e74aad-9994-4445-a7fa-8f2c99e51da5.png)

### Experiments

### Notes
