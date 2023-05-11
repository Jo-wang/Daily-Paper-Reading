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
<img width=400 alt="1683765342294" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/05cf4d06-8d1f-4077-9059-65e0315ad0b3">

<img width=400 alt="1683509941416" src="https://user-images.githubusercontent.com/46414159/236715575-268b5eaa-5174-446f-bb8e-3f78d1116a08.png">

#### TTBA
<img width=400 alt="1683766358057" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e0b7b38c-0638-4e66-bcc3-680d4f8d1616">

<img width=350 alt="1683531215912" src="https://user-images.githubusercontent.com/46414159/236763425-c5e74aad-9994-4445-a7fa-8f2c99e51da5.png">

#### OTTA
<img width=400 alt="1683775023507" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2e216451-d341-4fd9-a037-4f61d489533b">

<img width=350 alt="1683591032411" src="https://user-images.githubusercontent.com/46414159/236962657-4a656dd9-45d0-449f-a508-9c65620f7f07.png">

#### TTPA
<img width=350 alt="1683775165118" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/36081f99-c8e9-4f0d-9490-180f9a29e4b5">

