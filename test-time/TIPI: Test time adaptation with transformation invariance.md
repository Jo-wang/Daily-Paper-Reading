## [TIPI: Test time adaptation with transformation invariance](https://openaccess.thecvf.com/content/CVPR2023/papers/Nguyen_TIPI_Test_Time_Adaptation_With_Transformation_Invariance_CVPR_2023_paper.pdf)

CVPR2023

### Introduction and background
- Target data batch size is always small in real world.
- Previous surrogate loss is not optimal since it often collapses with small batch size.

### Method

<img width=300 alt="alg" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1f779d28-2228-48be-b424-9e08fc49d729">

- Modify the model during testing as two BN layers if there's BN in original model. One is for the statistic of $x$ and another is for $x^{\prime}$. But they share the affine parameter.

- Uses invariance regularization:
 
 <img width=260 alt="img" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7cd363d9-6e76-4eb6-a4c3-fc7f4e5c8e1f">

 where $p_T$ is the distribution of a transformation will be sampled. $x^{\prime}$ is the transformed target data. This is a inversed KL.

- The transformation is obtained from single-step adversarial method FGSM. (PGD will be more better.) 

### Experiments
- CIFAR10C/100C; ImageNetC; Digits; VisDA17

<img width=560 alt="img2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d620bac4-1892-4e36-ba8b-392483dd2c80">

### Notes
