## [Continual Test-Time Domain Adaptation](https://openaccess.thecvf.com/content/CVPR2022/html/Wang_Continual_Test-Time_Domain_Adaptation_CVPR_2022_paper.html)

CVPR2022

### Introduction and background
The motivation of this paper is to address the challenges of adapting a source pretrained model to a continually changing target domain, which is a common scenario in real-world machine perception systems. The specific motivations are:

- 1. Existing works mainly consider the case where the target domain is static, while real-world environments are non-stationary and continually changing.
- 2. Existing methods, which are mostly based on self-training and entropy regularization, can suffer from unreliable pseudo-labels in continually changing target domains.
- 3. The proposed approach aims to overcome these limitations by incorporating a weight-and-augmentation-averaged strategy and stochastic restoration into any pre-trained model without the need to re-train it on source data.

### Method
1. Initialize an off-the-shelf source pretrained model on the source domain.

2. Receive a sequence of target data in a continually changing environment.

3. For each new target sample, generate multiple augmented versions and average their predictions with the original model's prediction using a weight-and-augmentation-averaged strategy.

4. Use stochastic restoration to refine the averaged prediction by adding noise to it and then denoising it with a learned denoiser network.

5. Update the model's parameters online based on the current target data using backpropagation and stochastic gradient descent.

6. Repeat steps 3-5 for each new target sample in the sequence.

7. Output predictions in an online fashion.

### Experiments

### Notes
