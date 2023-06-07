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
Propose a class-balanced memory bank M with size N. 

<img width=400 alt="img2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2dd86413-ee9a-4863-a295-0c22ae332b4a">

Eq 6 is Heuristic score: $\mathcal{H}=\lambda_t \frac{1}{1+\exp (-\mathcal{A} / \mathcal{N})}+\lambda_u \frac{\mathcal{U}}{\log \mathcal{C}}$
 Attach each sample in M with a group of heuristics $(\mathcal{A}, \mathcal{U})$, where $\mathcal{A}$, initialized as 0 and increasing with time t, is the age of the sample, and $\mathcal{U}$ the uncertainty calculated as the entropy of the prediction. (apparently use this to avoid uncertain and imbalance sample to be saved in the memory bank)
 
#### Robust training with timeliness
- Use mean teacher only update the parameters in RBN where teacher is used to update the memory bank.
- Student have the strong augmented view and teacher have the weak one. Use CE to update: <img width=300 alt="img3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/db5faea7-03ec-42d8-bb47-616e6db036b7">
  
  where $p_S\left(y \mid x_i^{\prime \prime}\right)$ is the prediction from student model with strong augmentation.
  
- Teacher model is updated by EMA.
- The CE loss above will be weighted by $E\left(\mathcal{A}_i\right)=\frac{\exp \left(-\mathcal{A}_i / \mathcal{N}\right)}{1+\exp \left(-\mathcal{A}_i / \mathcal{N}\right)}$, which is the timeliness reweighting term. ($\mathcal{A}$ is the age as explained in CSTU)

- $\mathcal{L}\left(x_i^{\mathcal{M}}, \mathcal{A}_i ; \theta_t^T, \theta_t^S\right)=E\left(\mathcal{A}_i\right) \ell\left(x_i^{\prime}, x_i^{\prime \prime}\right)$
### Experiments

### Notes
