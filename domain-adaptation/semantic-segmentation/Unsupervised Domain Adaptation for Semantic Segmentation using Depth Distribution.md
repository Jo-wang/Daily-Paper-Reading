## [Unsupervised Domain Adaptation for Semantic Segmentation using Depth Distribution](https://openreview.net/forum?id=SLA4t66xln9)
NeurIPS2022

Ranking: 2.7

### Introduction and background
- Depth information is important but ignored by previous works
- Different semantic classes have their own depth distribution in images
- Main idea: 
  - 1. Use Gaussian mixture models (GMMs) to build the depth distribution for different semantic classes
  - 2. use the multi-task learning framework to learn three sub-tasks, i.e. semantic segmentation prediction, depth regression and depth distribution density estimation.
  - 3. use density estimation to balance the other two sub-tasks, mainly to improve the efficiency of the
main task(semantic segmentation)

### Method
![1670820688589](https://user-images.githubusercontent.com/46414159/206963272-b8e95f57-54be-46b0-86c0-ef56ad1fc02e.png)   
- **Supervised Learning**: 1. Semantic segmentation prediction by CE loss.2. Depth Regression by berHu loss:
![1670821176402](https://user-images.githubusercontent.com/46414159/206964190-b7d2b2d0-35d4-42e6-8e4b-d65acd42492e.png)
![1670821189442](https://user-images.githubusercontent.com/46414159/206964216-f1e0672f-1a60-4c60-a647-2f8e17379f79.png)
where $Z$ is the gt depth map.
- **Depth Distribution Density Estimation**: Source does has depth info, this information can be
used to construct Gaussian mixture models for each semantic category. (x, y, z) is a tuple of position (x, y) and the depth value z. We can learn GMM from source. The density values of each pixel: ![1670821714071](https://user-images.githubusercontent.com/46414159/206965156-865bda4f-2995-486d-a457-57c146310f72.png)
where the associated pixel that classified as ith class can be denoted as $\vec{X_{}i}$, $\mu$ is mean and $\Sigma$ is variance.    
A branch balance loss is used for the depth distribution density regression:
![1670823785848](https://user-images.githubusercontent.com/46414159/206969145-32c3d865-a33e-40fc-a1d4-c289b8dc820f.png)![1670823814399](https://user-images.githubusercontent.com/46414159/206969188-50d1e282-a8b9-4c49-a96c-d97dc6fe2711.png)
- **Adversarial Training**: use segmentation to fuse density map.
![1670824037600](https://user-images.githubusercontent.com/46414159/206969635-d16ceffd-e1ae-466c-9c74-d3eae1aca35f.png)
- **Spatial Aggregation Priors for Pseudo-labels Refinement**: calculate the total proportion of class-wise pixels in the source images as a prior to setup the threshold of pseudo labeling.
![1670824193732](https://user-images.githubusercontent.com/46414159/206969956-133e5d2a-e43e-414d-8b5a-5f0626760f34.png)
$N_{min}$ and $N_{max}$ represent the minimum and maximum numbers of pixels of different categories from all source samples. $N_{base0}=50$ and $N_{base1}=4950$.
### Experiments
- Dataset:  SYNTHIA → Cityscapes (16 classes), SYNTHIA → Cityscapes (7 classes),
and SYNTHIA → Mapillary (7 classes).
![1670824389085](https://user-images.githubusercontent.com/46414159/206970375-044a140f-60cc-4dab-8aa4-a4a4fed81774.png)

### Notes
![1670824461809](https://user-images.githubusercontent.com/46414159/206970523-5a6b658d-ee90-46c8-a793-f5d602f283e2.png)
