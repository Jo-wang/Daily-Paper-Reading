## [SOLO: Segmenting Objects by Locations](https://arxiv.org/pdf/1912.04488.pdf)

ECCV2020

Ranking: :star: :star: :star: :star:

### Introduction and background
- it is challenging to predict instance labels on pixel-level
- Previous methods is "detect-then-segment" e.g., Mask R-CNN, PANet, Mask Scoring R-CNN, HTC; or, predict embedding vectors first then use clustering techniques to group pixels into individual instances, e.g., SGN, SSAP
- Previous methods are step-wise and indirect, which either heavily rely on accurate bounding box detection or depend on per-pixel embedding learning and the grouping processing
<img width="600" alt="1675047335019" src="https://user-images.githubusercontent.com/46414159/215377897-50f95f7a-8696-423d-a5c4-1b9de8d73889.png">

- SOLO can directly segment (e.g., AdaptIS, PolarMask) the instance masks.End-to-end.

### Method
- Divide the image into uniform grids (S*S). If the center of an object falls into a grid cell, that grid cell is responsible for

  - predicting the semantic category (belongs to which class, so S*S -> S*S*C
  - segmenting that object instance (the seg map, S*S -> $H_I*W_I*S^2$
  
### Experiments

### Notes
