
## [Active Boundary Loss for Semantic Segmentation](https://ojs.aaai.org/index.php/AAAI/article/view/20139)

AAAI2022

Ranking: ⭐ ⭐ ⭐ 🌟

### Introduction and background
<img width="900" alt="Screen Shot 2023-01-17 at 22 22 04" src="https://user-images.githubusercontent.com/46414159/212897902-3a2f3296-91e4-455a-8529-55edcca3cd7c.png">

- the segmentation results might be blurred and lack ﬁne object boundary details
- boundary-aware information ﬂow control and multi-task training methods have been proposed to improve the discriminative power of features belonging to different objects
- there still exist a signiﬁcant amount of segmentation errors at object boundaries, especially for small and thin objects
- Main Steps:
  - for a pixel on the PDBs (predicted boundaries), we ﬁrst determine a direction pointing to the closest GTB (gt boundaries) pixel
  - then move the PDB at this pixel towards the direction in a probabilistic manner
  - detach the gradient ﬂow to suppress possible conﬂicts
  - 
### Method
<img width="950" alt="Screen Shot 2023-01-17 at 22 39 10" src="https://user-images.githubusercontent.com/46414159/212901216-bca60ea3-a167-4cad-9859-d1c91e4955f9.png">


### Experiments

### Notes
