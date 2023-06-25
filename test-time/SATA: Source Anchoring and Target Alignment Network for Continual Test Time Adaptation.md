## [SATA: Source Anchoring and Target Alignment Network for Continual Test Time Adaptation](https://arxiv.org/abs/2304.10113)


### Introduction and background
- 1) For online adaptation, the models should work seamlessly with different (preferably small) batch sizes, which reduces the inference time and latency;
- 2) The updated model should continue to work well in the source domain;
- 3) The framework should require less storage and minimal tunable hyper-parameters since validation sets are usually unavailable during test time.

- This paper focuses on online-continual TTA while testing the gradual TTA setting.
  
### Method
<img width=700 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1845f44d-3c51-4467-85cc-e533f9affc0d">

#### Source Anchorization of Model
Let $p_{ij}$ and $a_{ij}$ denote the $j$-th element of $f^k_{\theta_s}(x_i)$ (adapting model) and $f^k_\theta(x_i)$ (source model), respectively (j-th softmax output, which means the predicted probability of $x_i$ belongs to class j), and $q_{ij}$ be the j-th element of the augmented test sample. C is the number of classes, $N_k$ is the number of samples per batch, and $k$ is the batch, we calculate the loss in a entropy manner:

<img width=250 alt="e" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/747d14a8-cacf-405b-88c4-cce40741aeac">

#### Source-Guided Target Alignment
Assume the model during testing is defined as: $f_\theta^k=h \circ g_\phi^k$, where $h$ is the classifier, we project the feature: $z_i=p_\psi \circ g_\phi^k\left(x_i\right)$ from feature extractor $g_\phi^k$ to a projection head $p_\psi$, we use source prototype $\{\pi_i\}_{i=1}^C$

Then the test data, augmented test data and their corresponding source prototype are in the same batch. The batch size becomes $3N_k$, actually.

Then use contrastive learning-like loss:

<img width=300 alt="f" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4caedeba-2dde-4366-b993-8860bdc60891">

       
<img width=300 alt="fh" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d7a4dc56-dede-45fe-aa75-b6cca6658d09">


The overall loss: $\mathcal{L}_{SATA} = \mathcal{L}_{SA} + \mathcal{L}_{TA}$

### Experiments
- CIFAR10C/100C; ImageNet-C
- online continual/gradual
### Notes
