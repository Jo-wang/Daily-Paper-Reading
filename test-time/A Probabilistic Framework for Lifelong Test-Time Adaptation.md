## [A Probabilistic Framework for Lifelong Test-Time Adaptation](https://arxiv.org/abs/2212.09713)

CVPR2023

### Introduction and background
- Previous works assume the target domain is stationary, but test input distribution may exhibit a lifelong/continual shift over time.
- Existing TTA approaches also lack the ability to provide reliable uncertainty estimates, which is crucial when distribution shifts occur between the source and target domain.

### Method
<img width=700 alt="framework" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/72115b4b-377d-427e-ae67-652aa32cd4c8">

<img width=400 alt="alg1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b70ee7c4-9555-40e9-98a7-ba1526c6a0cd">

<img width=400 alt="alg2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d5b01332-2e59-4f94-95d9-ca65e47d8700">

Use SWAG-D to approximate the posterior density from the source domain training data.

$H^{xe}$ is the conditional cross-entropy of labels conditioned on the inputs. 

If the teacher prediction is confident, use the prediction of augmented data as $y^{\prime}$, else, use the average of all agumentations of one data sample $x$ as $y^{\prime}$.

Fisher matrix measure the amount of information for parameter estimation. If $F_p$ < $\gamma$, the useful info for current parameter is less, so we reset back to the source pretrained parameter.
### Experiments
- Setting: continual/gradual adaptation
- Dataset: CIFAR10C/100C; ImageNet-C; ImageNet3DCC
### Notes
