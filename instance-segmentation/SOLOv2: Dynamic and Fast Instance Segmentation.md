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
#### Dynamic instance segmentation
- The masking learning in SOLOv1 spend too much unneeded computation. To improve that, SOLOv2 uses dynamic masking.
- $M_{i,j}=G_{i,j}\times F$, where $G_{i,j}$ is the dynamic kernel learned, different grid will have different kernel parameters. $F$ is mask feature.
- 
#### Matrix NMS

### Experiments

### Notes
