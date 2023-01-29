## [Cut and Learn for Unsupervised Object Detection and Instance Segmentation](https://arxiv.org/abs/2301.11320)


Ranking: :star: :star: :star: :star:

### Introduction and background
- Object localization is a critical task
- Training models for localization require special annotations like object boxes, masks, localized points, etc. which are both difficult and resource intensive to collect. 
- vanilla NCut is limited to discovering a single object in an image (so as TokenCut)
### Method
- Use MaskCut generate multiple binary masks per image
using self-supervised features from DINO 
- Use a dynamic loss dropping strategy, called DropLoss, to learn a detector from MaskCut’s initial masks while encouraging the model to explore objects missed by MaskCut
- Use self-training for multiple rounds to further improve the performance

### Experiments

### Notes
- Normalized Cuts: https://blog.csdn.net/qq_43349296/article/details/122222469
- DINO: https://zhuanlan.zhihu.com/p/371735639
- ToeknCut: https://blog.csdn.net/u014546828/article/details/125179845
