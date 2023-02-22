## [Transferability Estimation Using Bhattacharyya Class Separability](https://openaccess.thecvf.com/content/CVPR2022/html/Pandy_Transferability_Estimation_Using_Bhattacharyya_Class_Separability_CVPR_2022_paper.html)

CVPR2022

Ranking: 

### Introduction and background
- without performing finetuning, it is difficult to quantify which pre-trained source models are suitable for a specific target task

### Method
<img width="400" alt="Screen Shot 2023-02-22 at 22 27 59" src="https://user-images.githubusercontent.com/46414159/220619791-e6313e37-0852-4e52-8d0a-b3aca059c1a6.png">
Main idea: measure the amount of overlap between target classes in the feature space of the source model

#### Formal description
The goal is to estimate the transferability score $S_{s→t}$ of a source model $m_s$ for a particular target task t. The target task t is described by a training set $D_t$ containing images and ground truth label pairs ($x_t$, $y_t$).

A good transferability metric $S_{s→t}$ correlates with the accuracy $A_{s→t}$ of the target model $m_{s→t}$. The accuracy $A_{s→t}$ is measured by evaluating $m_{s→t}$ on the (unseen) test set of the target task $D^{\text{test}}_t$.

Evaluating: weighted Kendall tau rank correlation $τ_w$

#### Class separability

<img width="400" alt="Screen Shot 2023-02-22 at 22 36 07" src="https://user-images.githubusercontent.com/46414159/220621402-76bdb83c-95dc-4086-a033-c9ba99e90fa2.png">

The key idea behind our method is that if the target images are class-wise separable in the source model feature space, then this source model allows for good classification for the target task.

**Bhattacharyya coefficient.** a measure of overlap between two distributions   
To measure two target class:

<img width="300" alt="Screen Shot 2023-02-22 at 23 19 56" src="https://user-images.githubusercontent.com/46414159/220631763-39e1ff50-051b-4df5-9914-71cb9a2aea46.png">

**Per-class Gaussian distributions.**

<img width="300" alt="Screen Shot 2023-02-22 at 23 24 15" src="https://user-images.githubusercontent.com/46414159/220632684-3a611ecd-630e-44b2-8996-4b92f61d9c23.png">

According to its property, we can transfer Bhattacharyya distance to Bhattacharyya coefficient (and that's also why we use Gaussian in this case):

<img width="700" alt="Screen Shot 2023-02-22 at 23 28 31" src="https://user-images.githubusercontent.com/46414159/220633688-66ed6cdf-a8ee-401d-8593-4a70ecaa0f5e.png">

---------------------------------------------

<img width="400" alt="Screen Shot 2023-02-22 at 23 30 42" src="https://user-images.githubusercontent.com/46414159/220634123-db786543-d55c-4a03-8abe-b8d00f19ac85.png">

**Gaussian Bhattacharyya coefficient.**
<img width="400" alt="Screen Shot 2023-02-22 at 23 44 11" src="https://user-images.githubusercontent.com/46414159/220637486-93154256-3386-4083-97e1-a8091324fe9b.png">

The negative sign because high coeff means high overlap, which is worse on target.

####

### Experiments

### Notes
