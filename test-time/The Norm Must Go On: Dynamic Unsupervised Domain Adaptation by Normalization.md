## [The Norm Must Go On: Dynamic Unsupervised Domain Adaptation by Normalization](https://openaccess.thecvf.com/content/CVPR2022/papers/Mirza_The_Norm_Must_Go_On_Dynamic_Unsupervised_Domain_Adaptation_by_CVPR_2022_paper.pdf)

CVPR2022

### Introduction and background
- **This paper focusing on OTTA: continuous dynamic adaptation**
- Related approaches typically ignore the training statistics and recalculate the batch statistics from scratch for the test data, which requires large batches of test data.
- This work require only a small number of sequential samples (less than 1% of unlabeled test data)
- This work requires no back propogation.

### Method
![1683597402630](https://user-images.githubusercontent.com/46414159/236974604-8fe0cd77-2322-4c31-8e23-d9b4d1ccd9f4.png)
The origional strategy would be updating the running mean and variance by a fixed momentum factor $$p$$

<img width=350 alt="1683610784039" src="https://user-images.githubusercontent.com/46414159/237004294-aac80ed9-ef1f-4591-9996-ba75f4fbbc71.png">

Here, they instead using an adjustable momentum parameter:
![1683611034608](https://user-images.githubusercontent.com/46414159/237004696-a93c4bf3-4bd5-4533-937b-7888a7e6177a.png)

with a decay factor $$w$$, and the figure below shows it could stabialize the running mean and variance during test-time.

![1683611162832](https://user-images.githubusercontent.com/46414159/237005034-8b954a7c-7a82-460d-88ff-db5d3b6a4269.png)

### Experiments
- Dataset: CIFAR-10/100C; ImageNet-C; KITTI; Digit Recognition; Office-31; VIS-DA; SODA10M
![1683611558189](https://user-images.githubusercontent.com/46414159/237006124-fa9096d9-945f-44a0-9af4-1c5eb5c124cc.png)
![1683611609861](https://user-images.githubusercontent.com/46414159/237006282-16eec72f-9196-4f6d-b7c4-b801db1f16db.png)

- Continuous Dynamic Adaptation (object detection): KITTI-Fog: day→fog→day→etc
- ![1683611420086](https://user-images.githubusercontent.com/46414159/237005794-82aecd42-e15d-4695-b75f-6a08892c3152.png)

