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
- projection head consists of two sub-heads in parallel, which are global projection head (takes the dense feature maps as input and generates a global feature vector for each view) and dense projection head (takes the same input but outputs dense feature vectors) respectively

#### Dense Contrastive Learning
- the query r are all local part of a view, the encoded keys are $t_0 , t_1 \cdot$
- positive keys are assigned accortding to the extracted correspondence across views (from other views of the same image)
- negative keys are pooled feature vertor of a view from a different image
<img width="400" alt="1675734893494" src="https://user-images.githubusercontent.com/46414159/217127985-fd65cdf3-b322-4917-a239-03e08246be01.png">

#### Dense Correspondence across Views
- Using cosine similarity: each feature vector in a view is matched to the most similar feature vector in another view
<img width="400" alt="1675735347585" src="https://user-images.githubusercontent.com/46414159/217128949-27af4670-c1b7-47b8-8c7c-7c9e509b5930.png">

### Experiments
- dataset: MS COCO, and ImageNet
<img width="400" alt="1675735614462" src="https://user-images.githubusercontent.com/46414159/217129501-bd2aa24b-07b0-4cb7-846d-34ab9bbd2c0e.png">
<img width="400" alt="1675735652789" src="https://user-images.githubusercontent.com/46414159/217129587-2d4fd4a6-643b-457c-b07d-ea4db6491a97.png">

### Ablation Study
<img width="400" alt="1675735728097" src="https://user-images.githubusercontent.com/46414159/217129761-6d5545b2-5fed-435d-9d58-bdb24f7656eb.png">

<img width="800" alt="1675735761112" src="https://user-images.githubusercontent.com/46414159/217129851-4e1d850d-0b8d-4e64-a99d-71ae091205d4.png">

<img width="400" alt="1675735782308" src="https://user-images.githubusercontent.com/46414159/217129899-e0b311f0-a371-43cf-9d5a-c9384a2930a2.png">

<img width="400" alt="1675735797928" src="https://user-images.githubusercontent.com/46414159/217129927-c03e2ca7-139f-4b37-80e5-1bc3366e60b1.png">

<img width="400" alt="1675735813911" src="https://user-images.githubusercontent.com/46414159/217129958-ee28d7ec-dc78-4d0b-9623-b6033eafda6f.png">
