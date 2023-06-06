## [TeSLA: Test-time self-learning with automatic adversarial augmentation](https://www.notion.so/TeSLA-Test-time-self-learning-with-automatic-adversarial-augmentation-a8425478f0d34f3d904c65843685b1f6?pvs=4)

CVPR2023

### Introduction and background
- most of SFDA or TTA methods are applied: 
  - (i) only to classification tasks
  - (ii) evaluated on the non-real-world domain shifts, e.g., the non-measurement shift
  - (iii) destroy model calibration—entropy minimizing with overconfident predictions on incorrectly classified samples
  - (iv) use specialized network architectures or rely on the source dataset feature statistics

### Method
- **Flipped Cross Entropy Loss**: <img width=200 alt="image" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/efc93f95-e82c-4709-b40c-5199f6e789a7">

  where $Y$ is student model prediction and $\hat{Y}$ is soft pseudo label predictions from teacher model
  
  it could be then writen as:
  
  <img width=400 alt="image1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ed7c7418-10ea-4bd2-8cc3-07fd95614774">
  
  where $f_s$ is student model and 
  
  <img width=150 alt="image3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2531df69-61c5-4309-8614-c822b571f434">

- **KD via Augmentation**:
  - Consistency between student and teacher: 
  
    <img width=200 alt="image4" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b88f8efa-70a6-4a39-93f8-736af529b948">
    
    where $\tilde{x}$ is the **learned adversarial augmented view** (introduced below) of $x$, $\hat{y}$ is the soft pseudo label below.
    
  - Soft pseudo label refinement: refine the quality of soft pseudo-labels and the feature representations by
averaging the teacher model’s outputs on multiple weakly augmented image views $\rho_w(\boldsymbol{x})$
    
    <img width=250 alt="image5" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a29d54d6-203f-47ff-9121-99ac5a403f8d">, where g is encoder and h is the classifier. Then both z and y will be saved in an online memory queue Q.
    
    The final soft pseudo-label is computed by averaging the refined soft pseudo-labels of n-nearest neighbors of the current test image in the feature space
    
    <img width=200 alt="image6" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6ecdc6f6-1d12-48d2-a2d9-4757e7453037">, where $\mathcal{N}_{\mathbf{Q}, n}\left(\mathbf{z}_t\right)$ is the soft labels of n-nearest neighbor of $z_t$ from Q.


    
  
- **Adversarial Data Augmentation**:
  - The adversarial data augmentation will be applied above for prediction consistency.
  - Define all image transformations as a set O. 
  - <img width=200 alt="image7" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cc256f92-a15d-41c3-945e-ca5a39f16452"> where $\rho$ combined with N image operation as a sub-policy. $m^\rho= [m_1^\rho, \ldots, m_N^\rho ]$ is the magnitude set of the sub-policy. $\mathbb{P}=\rho_1, \rho_2, \ldots $ are all sub-polities.
  - The sub-policy will be optimized by 
  
    <img width=250 alt="image8" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/98bed738-b14c-46b6-83e0-1982d38a24ec">
    
    max the ent to push its feature representation towards the decision boundary. 
    
    <img width=250 alt="image9" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3ef72a6d-275d-4fa3-bd98-be4ecc26cd69">
    
  - Optimize policy: <img width=250 alt="image10" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2bcf0c35-cf65-4b79-978c-7a35d46ba613">
    
    where <img width=250 alt="image10" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/0fe1f97a-08c3-41cb-93aa-e7937f5b772a"> 
    
    is the unbiased estimator of the expection of the loss aug for all policy.

**Overall loss**: <img width=300 alt="image10" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/c6ff7482-5553-48ca-8602-ab379b408f24">

### Experiments

### Notes
