## [Segfix: Model-agnostic boundary refinement for segmentation](https://arxiv.org/abs/2007.04269)

ECCV2020

:star: :star: :star:

### Introduction and background
<img width="800" alt="1674016310238" src="https://user-images.githubusercontent.com/46414159/213084550-399d2f8f-5e14-4d98-9ea5-9f1c0e41f48b.png">

- Most of the existing state-of-the-art segmentation models fail to deal well with the error predictions along the boundary.


### Method
![1674017669505](https://user-images.githubusercontent.com/46414159/213087389-2b41845d-d8c7-4396-8598-d54841646678.png)
- 1. Obtain feature map $X$ of the sample, 
  - put it in boundary branch to predict a binary map $B$. 1 is boundary and 0 is not boundary (use BCE)
  - put $X$ also in the direction branch to predict a direction map $D$ with each element storing the direction pointing from the boundary pixel to the interior pixel. (use CE)
  - the direction map $D$ is then masked by binary map $B$ to yield the input for the offset branch.
- 2. Testing stage: apply the offset branch to generate a offset map ∆Q. A coarse label map $L$ is output by any semantic segmentation model will be refined as:
  <img width="800" alt="1674019847207" src="https://user-images.githubusercontent.com/46414159/213091958-96167c19-8b46-4ef7-8ca9-e66a1986cbd6.png">      
  Also, some boundaries are thick, we can rescale all the offset by a factor 2.

  refinement
  <img width="700" alt="1674020494428" src="https://user-images.githubusercontent.com/46414159/213093294-fd72d15e-d329-4db6-a408-d80a56764306.png">

### Experiments

### Notes
