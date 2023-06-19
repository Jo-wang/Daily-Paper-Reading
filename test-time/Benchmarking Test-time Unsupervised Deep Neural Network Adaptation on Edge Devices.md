## [Benchmarking Test-time Unsupervised Deep Neural Network Adaptation on Edge Devices](https://arxiv.org/abs/2203.11295)

ISPASS2022

### Introduction and background
- Benchmarking the TTA on edge devices for two basic algorithms and testing performance and energy.

### Method
- Two algorithms: 1. BN with optimization (update both $\mu$ $\sigma$ and affine parameter); 2. only update the BN statistic parameter
- Two evaluation metrics: performance and energy
- Three backbones: Resnet-18; WRN-40-2; ResNeXt29_32*4d
- One dataset: CIFAR-10-C-level 5
- Batch size: 50, 100, 200
- Devices: Ultra96_v2 FPGA; Raspberry-Pi; Nvidia Jetson Xavier NX

### Experiments
Please see the paper
