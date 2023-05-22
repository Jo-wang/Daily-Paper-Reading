## [Continual Test-Time Domain Adaptation](https://openaccess.thecvf.com/content/CVPR2022/html/Wang_Continual_Test-Time_Domain_Adaptation_CVPR_2022_paper.html)

CVPR2022

### Introduction and background
The motivation of this paper is to address the challenges of adapting a source pretrained model to a continually changing target domain, which is a common scenario in real-world machine perception systems. The specific motivations are:

- 1. Existing works mainly consider the case where the target domain is static, while real-world environments are non-stationary and continually changing. (may have forgetting issue for source data)
- 2. Existing methods, which are mostly based on self-training and entropy regularization, can suffer from unreliable pseudo-labels in continually changing target domains. (may accumulate error)
- 3. The proposed approach aims to overcome these limitations by incorporating a weight-and-augmentation-averaged strategy and stochastic restoration into any pre-trained model without the need to re-train it on source data.

### Method

<img width=350 alt="1684757605062" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/20f0bdc0-adef-4f08-a3ca-bda208edab3e">

<img width=350 alt="1684758750798" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2b54b51d-4b5b-477d-9778-acf1d3637e96">

1. Initialize an off-the-shelf source pretrained model on the source domain.

2. Receive a sequence of target data in a continually changing environment.

3. For each new target sample, generate multiple augmented versions and average their predictions with the original model's prediction using a weight-averaged strategy. Teacher model with augmentation, use teacher model to get pseudo label and use CE loss between student and teacher prediction to update the model.

<img width=350 alt="1684757914348" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b4cc6a6a-d751-4a29-9508-6cb9a25d602f">

Then use EMA to update the teacher.

4. Use Augmentation-Averaged Pseudo-Labels: consider test-time domain shift and approximate
the domain difference by prediction confidence, augmentation is only applied when the domain difference is large, to reduce error accumulation.

<img width=350 alt="1684758295694" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cc406758-8b25-4461-a5c0-bb4ee89d5a61">

When the confidence is low, we apply additionally N random augmentations to further improve the pseudo-label quality.

5. Use stochastic restoration to refine the averaged prediction by adding noise to it and then denoising it with a learned denoiser network.

For a conv layer weight at t+1 step called $w_{t+1}$, we stochastic restore the weight from the source weight $w_0$ by: 

<img width=350 alt="1684758696345" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/0c096146-12a0-4f0f-840d-069d8ec35c70">

5. Update the model's parameters online based on the current target data using backpropagation and stochastic gradient descent.

### Experiments

### Notes
