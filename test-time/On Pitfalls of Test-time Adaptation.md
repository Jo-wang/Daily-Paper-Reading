## [On Pitfalls of Test-time Adaptation](https://arxiv.org/pdf/2306.03536.pdf)

ICML2023

### Introduction and background
- The motivation of this paper is to address the challenges and limitations of Test-Time Adaptation (TTA) in machine learning. 
- The authors aim to provide a comprehensive analysis of the pitfalls of TTA and propose a benchmark library, called TTAB, to standardize experimental settings and evaluate the effectiveness of TTA algorithms across a broader range of base models and distribution shifts. 
- The authors hope that their work will not only facilitate rigorous evaluations of TTA algorithms but also stimulate further research into the assumptions that underpin the viability of TTA in challenging scenarios. 

### Method
<img width=650 alt="1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/c0d44a09-91d1-4962-b4a5-eeafd86438f1">

<img width=650 alt="2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/573b2bc8-5e8f-42cb-a303-d1acb67d713c">

### Experiments
- CIFAR10C/100C; ImageNet-C; PACS, CIFAR10.1; ColoredMNIST; OfficeHome
- ResNet-18/ResNet26/ResNet-50 as the base model on ColoredMNIST/CIFAR10-C/large-scale image datasets
- online/episodic; Aux regularization; batch dependency; checkpoint selection; pretrained model (feature extractor; classifier; augmentation); domain shift (common distribution shift: covariant shift,natural shift, DG; spurious correlation shift; label shift; non-stationary shift)
### Notes
