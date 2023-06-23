## [ActMAD: Activation Matching to Align Distributions for Test-Time-Training](https://arxiv.org/pdf/2211.12870.pdf)

CVPR2023

### Introduction and background
- the approaches that minimise the entropy of test predictions or use pseudo-labels or pseudo-prototypes are not easily adapted to object detection or regression
- the ones that update the statistics of the batch normalization layers are limited to architectures that contain them


### Method
<img width=700 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3e1448d6-3902-40dd-92fe-30471333ecf3">

- the activation response of $l$-th layer of the network $f$ computed for image $x$ is $a_l (x;\theta)$
- we aim to separately align each of the C*W*H (feature map) activations in the $l$-th layer
- Then calculate the source statistics from different layers. For each layer's statistic, we align it with the test statistics by l1 norm.
- <img width=400 alt="a2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/044b631b-6c5f-4e2f-b935-99c3ffa49570">
- We set the final loss $L$ as the summation of all layers' loss $L_l$
- We plan to update the parameters for the whole network.
  
### Experiments
- Online w/o continual
- Dataset: CIFAR-10C/100C; ImageNet-C; KITTI
- Tasks: image classification, object detection

