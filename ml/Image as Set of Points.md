## [Image as Set of Points](https://openreview.net/pdf?id=awnvqZja69)

ICLR2023 oral

Ranking: :star: :star: :star:

### Introduction and background
- traditional image classification methods uses ConvNet or ViT. The former one assume the image structure as a rectangle and the latter assume image is a sequence of image patches.
- this method assume image is a set of points and propose Context Cluster borrowed the idea from point cloud and could be more generalizable.

### Method
#### Context Cluster Pipeline
- 1. image → coordinate → a collection of points (with both feature and x y position) → unorder them

- 2. feature extraction: 
  <img width="350" alt="1675824673666" src="https://user-images.githubusercontent.com/46414159/217416480-ad6d9dd6-75be-40fa-a907-95d008f5edf3.png">
  
  <img width="700" alt="1675824747749" src="https://user-images.githubusercontent.com/46414159/217416663-b2c11981-c9b6-47c4-b611-dc29da9cd8d3.png">

  - To reduce the points number, we evenly select some anchors in space, and the nearest k points are concatenated and fused by a linear projection. Note that this reduction can be achieved by a convolutional operation if all points are arranged in order and k is properly set.
  - For classification, average all points of the last block’s output and use a FC layer for classification. 
  - For downstream dense prediction tasks like detection and segmentation, we need to rearrange the output points by position after each stage to satisfy the needs of most detection and segmentation heads.
  
#### Conetxt Cluster Operation
- cluster all points according to the similarity between feature points and a center. we evenly propose c centers in space, and the center feature is computed by averaging its k nearest points. We then calculate the pair-wise cosine similarity matrix S ∈ $R^{c×n}$ between Ps and the resulting set of center points. we allocate each point to the most similar center, resulting in c clusters
- dynamically aggregate all points in a cluster based on the similarities to the center point. Map the points and the center into value space and the aggregated feature is:
<img width="700" alt="1675827097170" src="https://user-images.githubusercontent.com/46414159/217422631-e98da4e4-6205-4eff-af49-eb59ce1d7846.png">

<img width="700" alt="1675827925666" src="https://user-images.githubusercontent.com/46414159/217426248-de288f1b-42f6-49a0-b503-f5e3751726dc.png">


### Experiments
- dataset:on ImageNet-1K, ScanObjectNN, MS COCO, and ADE20k 
- tasks: image classification, object detection, instance segmentation, semantic segmentation
- experiments:
<img width="400" alt="1675828102837" src="https://user-images.githubusercontent.com/46414159/217427023-401459d3-990d-47a1-98f9-cae8d8029116.png">
<img width="700" alt="1675828118924"https://user-images.githubusercontent.com/46414159/217427101-b6affa45-8b1c-44e5-9f25-eec838a9a429.png">
<img width="300" alt="1675828141231" src="https://user-images.githubusercontent.com/46414159/217427172-eca01250-5eb2-494e-a8e6-3af210a95e50.png">



### Ablation Study
<img width="300" alt="1675828052807" src="https://user-images.githubusercontent.com/46414159/217426770-76894cb6-4f77-48c2-a91d-e57a2e4233c5.png">







