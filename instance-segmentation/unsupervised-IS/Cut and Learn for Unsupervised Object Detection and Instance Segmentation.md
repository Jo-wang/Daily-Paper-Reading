## [Cut and Learn for Unsupervised Object Detection and Instance Segmentation](https://arxiv.org/abs/2301.11320)


Ranking: :star: :star: :star: :star:

### Introduction and background
- Object localization is a critical task
- Training models for localization require special annotations like object boxes, masks, localized points, etc. which are both difficult and resource intensive to collect. 
- vanilla NCut is limited to discovering a single object in an image (so as TokenCut)
### Method
- **Use MaskCut generate multiple binary masks per image
using self-supervised features from DINO: **    
iteratively applying NCut to a masked similarity matrix. After getting the bipartition $x^t$ from NCut at stage t, we get two disjoint groups of patches and construct a binary mask $M^t$:
<img width="250" alt="1675043721894" src="https://user-images.githubusercontent.com/46414159/215371683-96b17c3d-de7c-4560-acf4-00a4dedce996.png">
  - If the group is foreground, we have: foreground mask should
contain the patch corresponding to the maximum absolute value in the second smallest eigenvector $M^t$; the foreground set should contain less than two of the four corners.
  - To update the node similarity in order to get the (t+1) object (because we obtain the objects iteratively), by default, t=3: 
  <img width="300" alt="1675043996663" src="https://user-images.githubusercontent.com/46414159/215372124-ce81b842-3760-47b7-b7c9-0b4fd58dd065.png">


- **Use a dynamic loss dropping strategy, called DropLoss, to learn a detector from MaskCut’s initial masks while encouraging the model to explore objects missed by MaskCut: **
  only the region has the overalpping rate larger than a threshold $T^{\text{IoU}}$ will use vanilla loss to train (to avoid the current background be penalized since there may undetected object in the current background)

- **Use self-training for multiple rounds to further improve the performance: ** use the predicted masks and proposals with a confidence score over 0:75−0:5t from the $t^{th}$-round as the additional pseudo annotations for the (t + 1)th-round of self-training. To de-duplicate the predictions and the ground
truth from round t, we filter out ground-truth masks with IoU > 0.5 with the predicted masks.

### Experiments

### Notes
- Normalized Cuts: https://blog.csdn.net/qq_43349296/article/details/122222469
- DINO: https://zhuanlan.zhihu.com/p/371735639
- ToeknCut: https://blog.csdn.net/u014546828/article/details/125179845
