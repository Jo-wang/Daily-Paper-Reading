## [SOLOv2: Dynamic and Fast Instance Segmentation](https://arxiv.org/abs/2003.10152)

NeurIPS2020

⭐ ⭐ ⭐ ⭐

### Introduction and background
- bounding boxes are coarse and unnatural
- most existing methods deal with instance segmentation in the view of bounding boxes
- For box-free SOLO, three main bottlenecks limit its performance: 
  - a) inefficient mask representation and learning; 
  - b) not high enough resolution for finer mask predictions; 
  - c) slow mask NMS.

### Method
<img width="600" alt="1675298447231" src="https://user-images.githubusercontent.com/46414159/216202450-91db7de0-2f79-469c-8d25-6b693d3cfa91.png">

#### Dynamic instance segmentation
- The masking learning in SOLOv1 spend too much unneeded computation. To improve that, SOLOv2 uses dynamic masking.
- $M_{i,j}=G_{i,j}\times F$, where $G_{i,j}$ is the dynamic kernel (d-dimensional parameters) learned, different grid will have different kernel parameters. $F$ is mask feature.
- **Mask Kernel G:** Given the backbone and FPN, we predict the mask kernel $G$ at each pyramid level.
  - 1. Resize the input feature;
  - 2. 4 convs + 3*3*D conv to generate kernel G;
  - 3. Give the first conv the normailzed coordinate x, y (CoordConv)
  - 4. For each grid, the kernel branch predicts the D-dimensional output to indicate predicted convolution kernel weights, where D is the number of parameters. If we have S*S grids, the corresponding output space is S*S*D.
- **Mask Feature F:** predict a unified mask feature representation for all FPN levels (feature pyramid fusion)
  - we feed normalized pixel coordinates to the deepest FPN level (at 1/32 scale), before the convolutions and bilinear upsamplings.
- **Forming instance mask:** For each grid cell at (i; j), we first obtain the mask kernel $G_{i;j;:}$. Then $G_{i;j;:}$ is convolved with F to get the instance mask. In total, there will be at most $S^2$ masks for each prediction level. 
#### Matrix NMS
- For a predicted mask $m_j$, its decay factor could be effected by:
  - The penalty of each prediction $m_i$ on $m_j$ ($s_i$  > $s_j$), where $s_i$ and $s_j$ are the confidence scores.  $\rightarrow$ monotonic decreasing function $f(iou)$
  - The probability of $m_i$ being suppressed. $\rightarrow$ the probability usually has positive correlation with the IoUs. So here we directly approximate the probability by the most overlapped prediction on $m_i$
  <img width="600" alt="1675301430417" src="https://user-images.githubusercontent.com/46414159/216208861-b5c91ea8-3b7d-4f48-9cdf-cd944855cf63.png">
  <img width="600" alt="1675303691754" src="https://user-images.githubusercontent.com/46414159/216213660-0800dd01-dbba-4d1f-bd3b-4ddda7f2092e.png">

### Experiments
- dataset: COCO test-dev; LVISv0.5
- rare APr, common APc and frequent categories APf
<img width="700" alt="1675302259942" src="https://user-images.githubusercontent.com/46414159/216210640-d01064f5-85f3-4fbf-9119-6b85543b29be.png">
<img width="700" alt="1675302301033" src="https://user-images.githubusercontent.com/46414159/216210705-4e336fef-bc33-4494-81f1-0d5d59605f44.png">

<img width="700" alt="1675302364540" src="https://user-images.githubusercontent.com/46414159/216210844-ccee9288-5d5a-4c21-b29b-1377f44cb2a5.png">


