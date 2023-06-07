## [Robust Test-Time Adaptation in Dynamic Scenarios](https://www.notion.so/Robust-Test-Time-Adaptation-in-Dynamic-Scenarios-23d0738e57134439b89c64e86e0b3f03?pvs=4)

CVPR2023

### Introduction and background
- Original TTA or SFDA fail in dynamic scenarios of real-world applications like autonomous driving, where the environments gradually change and the test data
is sampled correlatively over time.
<img width=550 alt="img" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d4387f26-4fe9-435e-8de1-be8e8e0dfb0e">

### Method
<img width=600 alt="img1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3d382f39-960d-44ad-8607-159484a79b26">

#### Robust batch normalization (RBN)
- EMA update the BN layer: $\mu_g =(1-\alpha) \mu_g+\alpha \mu$ and $\sigma_g^2 =(1-\alpha) \sigma_g^2+\alpha \sigma^2$, where $\mu$ and $\sigma$ is the statistics of current batch.
#### Category-balanced sampling with timeliness and uncertainty (CSTU)
#### Robust training with timeliness
### Experiments

### Notes
