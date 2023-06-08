## [EcoTTA: Memory-Efficient Continual Test-time Adaptation via Self-distilled Regularization](https://arxiv.org/abs/2212.09713)

CVPR2023

### Introduction and background
- The motivation behind the EcoTTA method is to improve continual test-time adaptation (TTA) in a memory-efficient manner. 
- TTA is important for edge devices with limited memory, but reducing memory consumption has been overlooked in previous TTA studies. 
- In addition, long-term adaptation often leads to catastrophic forgetting and error accumulation, which hinders applying TTA in real-world deployments. 

### Method

<img width=700 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e4f37a0d-d335-4b29-b7e2-ae53d1e64260">

#### Source pretraining
- Pretrain the source model in a simple supervised manner
- Freeze original pretrained model, Split the encoder of the pretrained model into K parts, for each part, insert a **meta network** consists of a BN and a Conv block (Conv + Bn + ReLU)
- Warm up the meta network for a small amount of epochs (10 epochs for CIFAR)

#### TTA
- Only adapt the meta network during adaptation (TinyTL shows that activations occupy the majority of the memory required for training the model rather than learnable parameters)

  <img width=180 alt="img" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e1c4567e-dabf-4016-b4cf-7af206794526">

- Use entropy minimization if the entropy is less than a predefined threshold $H_0$: <img width=150 alt="img2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ed10ad0d-de67-4374-b233-456628a8f3e9">

- Define a regularization term: regularize the output $\tilde{x}_k$ of each k-th group of the meta networks not to deviate from the output $x_k$ of the k-th part of frozen original networks: <img width=100 alt="img3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2033d42e-86ac-4d0c-963a-755516679c17">

  
### Experiments
- Image classification; semantic segmentation
- CIFAR10C/100C; ImageNet-C
- Cityscapes-C created by applying weather corruptions in this paper
- Continual learning without reset.

<img width=700 alt="img4" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7fb0d833-a227-43cd-ab41-18bf55e65a96">
<img width=300 alt="img5" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f6b86cc1-a852-4d0f-a3d8-f3688cd7d0c0">

### Notes
