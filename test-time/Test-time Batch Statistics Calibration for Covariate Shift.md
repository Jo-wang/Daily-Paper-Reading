## [Test-time Batch Statistics Calibration for Covariate Shift](https://arxiv.org/abs/2110.04065)

Not published yet

### Introduction and background
<img width=700 alt="1684913060886" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f0318225-cb98-44a5-b28d-d82ea5d3de5e">

- The authors note that test time normalization, a common technique for addressing covariate shift, may potentially deteriorate the discriminative structures of deep models due to the mismatch between target batch statistics and source parameters. 

- The proposed approach called α-BN addresses this issue and improves the adaptation of deep models to novel environments.

### Method
**1. Mix up the source and target statistics in batch normalization (BN) layers to alleviate domain shift and preserve discriminative structures. This is called α-BN.**

**2. Incorporate α-BN into mainstream deep neural networks to improve generalization on unseen domains without any training.**

 <img width=700 alt="1684913575131" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3a1260bb-bf14-4aa6-9ae0-b0cb27736e3e">

**3. Propose a unified framework called Core for robust and accurate test-time adaptation, which optimizes pairwise class correlation in an unsupervised online learning manner by the loss:**

 <img width=700 alt="1684913528465" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f73f5dbd-4344-4620-ba90-110b2f1b040d">


### Experiments
#### Task
- Img classification; DG for img classification; semantic segmentation

<img width=700 alt="1684910375042" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/498e5f35-8044-46c8-a93a-723d3e921d9c">

#### Dataset
- CIFAR10-C/100-C; Imagenet-C;
- VLCS, PACS, Office-Home and DomainNet
- GTA5 and SYNTHIA, Cityscapes, BDD-100K, Mapillary

#### backbone etc
- Resnet; WRN; Deeplabv3; AugMix

####
### Notes
