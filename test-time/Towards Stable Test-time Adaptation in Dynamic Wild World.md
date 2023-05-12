## [Towards Stable Test-time Adaptation in Dynamic Wild World](https://openreview.net/forum?id=g2YraF75Tj)

ICLR2023

Ranking: ⭐ ⭐ ⭐ 

### Introduction and background
![1683864036646](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1cc6a706-80c7-4bd9-9d53-e25a46c4831e)
- This is online setting, OTTA; also could be seen as 
- Conventional TTA may fail when facing with mixed domain shift; simgle sample batch; or online imbalanced label shift.
- Bn is the key obstacle
- pre-trained models with batch-agnostic norm layers (i.e., group norm (GN) and layer norm (LN) are more beneficial for stable TTA
- to avoid neg transfer, filter partial samples with large and noisy gradients out of adaptation according to their entropy
- propose sharpness-aware and reliable entropy minimization method to avoid side effect from GN and LN
### Method
![1683868077925](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/acb5888f-d696-4fd3-b0ec-2fc29c1c7a2f)

- Batch Normalization Hinders Stable TTA: batch-agnostic norm layers are more suitable for TTA
- Online Entropy Minimization Tends to Result in Collapsed Trivial Solutions, i.e., Predict All Samples to the Same Class
- 
#### Reliable Entropy Minimization
selecting samples with small loss values can remove part of samples that have large gradients out of adaptation (remove area 1 and area 2)

<img width=300 alt="1683867855451" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4cc7aa73-67ac-48d5-b1ae-56cab8fe4c26">

#### Sharpness-aware Entropy Minimization
we only want to optim area 3 since samples in area 4 still have large gradient and may harm adaptation. So make the model insensitive to the large gradients, encourage the model to go to a flat area of the entropy loss surface

![1683869195865](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/50f85a00-6be0-45cb-a875-b029bbb9bd4a)

To avoid extreme hard cases, uses Model Recovery Scheme: record moving average of ent loss, if is smaller than a thres, reset to previous step model parameter.

### Experiments
- ImageNet-C 
- arch: ResNet50-BN/GN; VitBase-LN
### Notes
