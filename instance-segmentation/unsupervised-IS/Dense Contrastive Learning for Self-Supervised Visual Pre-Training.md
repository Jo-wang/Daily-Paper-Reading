## [Dense Contrastive Learning for Self-Supervised Visual Pre-Training](https://openaccess.thecvf.com/content/CVPR2021/papers/Wang_Dense_Contrastive_Learning_for_Self-Supervised_Visual_Pre-Training_CVPR_2021_paper.pdf)

CVPR2021

(This paper is a basis of FreeSolo)

Ranking: :star: :star: :star: :star:

### Introduction and background
- self-supervised learning are designed and optimized for image classification tasks and can be sub-optimal for dense prediction tasks
- pre-training for dense prediction tasks makes annotation is
notoriously time-consuming compared to the image-level
labeling
- self-supervised learning that is customized for dense prediction tasks is on demand
- This paper:
  - 1 propose dense contrastive learning (DenseCL) for self-supervised visual pre-training
  - introduce a dense projection head that takes the features from backbone networks as input and generates dense feature vectors.
  - this method preserves the spatial information and constructs a dense output format
  - 2 define the positive sample of each local feature vector by extracting the correspondence across views
  - design a dense contrastive loss, which extends the conventional InfoNCE loss to a dense paradigm. 

### Method
#### Pipeline
- Given an input view, the dense feature maps are extracted by the backbone network and forwarded to the following projection head.
- projection head consists of two sub-heads in parallel, which are global projection head(takes the dense feature maps as input and generates a global feature vector for each view) and dense projection head (takes the same input but outputs dense feature vectors) respectively

#### Dense Contrastive Learning




### Experiments

### Notes
