
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
### Method
<img width="950" alt="Screen Shot 2023-01-17 at 22 39 10" src="https://user-images.githubusercontent.com/46414159/212901216-bca60ea3-a167-4cad-9859-d1c91e4955f9.png">   

#### Phase I      
- Use class probability map $P \in R^{C\times H\times W}$ to detect PDBs by the current network.
- compute a boundary map B through the computation of KL divergence to indicate the locations of PDBs. For a pixel i in B, its value $B_i$ is computed as follows:
  <img width="250" alt="1674003454334" src="https://user-images.githubusercontent.com/46414159/213054709-ebde8341-e31b-4fd3-ad88-75face640196.png">         
  where $N_2 (i)$ is the 2-neighborhood of pixel i. ϵ is an adaptive threshold to ensure that **the number of boundary pixels in B is less than 1% of the total pixels of the input image**, where 1% is a ratio to approximate the number of boundary pixels in an image. 

- for a pixel i on PDBs, its next candidate boundary pixel j is selected as its neighboring pixel **with the smallest distance value** computed by the distance transform (scipy.ndimage.morphology.distance_transform_edt) of the GTBs. 这个GTBs无需通过另外的edge detection得到，而是用上边的$B_i$ 但是 the KL divergence is replaced by checking whether the ground-truth class labels are equal between pixel i and $j \in N_2 (i)$.
- $j$ is defined by compute a target direction map 
  $D_g \in \{ 0,1 \} ^{8\times H\times W}$
  <img width="350" alt="1674005126093" src="https://user-images.githubusercontent.com/46414159/213058096-81d91e9c-0637-4800-9b5d-a0ad22a97467.png">

#### Phase II      
$D^g_i$ is set to be the target distribution in the cross entropy loss. The The idea is increase the KL divergence between the class probability distribution of **i and j**, and simultaneously **reduce the KL divergence between i and the rest of its neighboring pixels**. 

An 8D vector using the KL divergence between pixel i and its neighboring pixel j as logits, denoted by $D^p_i$:
<img width="350" alt="1674006227085" src="https://user-images.githubusercontent.com/46414159/213060698-e52ddccb-7b47-4902-8c10-d38a098b0044.png">



#### Conflict suppression      
<img width="350" alt="1674001955105(1)" src="https://user-images.githubusercontent.com/46414159/213049355-feefa2b3-5eea-48e0-b02d-d9b3ab3db559.png">
through the detaching operation, the gradient of ABL is computed only for the pixels on the PDBs, but not for its neighboring pixels. This process
indicates that, for a 3 $\times$ 3 patch, we focus on the adjustment
of the class probability distribution of pixels on the PDBs only so as to move the PDBs towards the GTBs.

Also set label smoothing to regularize the ABL by setting the largest probability of the one-hot target probability distribution to 0.8 and
the rest to 0.2/7 (the parameters, 0.8 and 0.2/7 are determined through experiments). 

#### Training Loss      
$L_t=\text{CE}+\text{IoU}+w_a \text{ABL}$ where IoU is lovasz-softmax loss.

### Experiments
- dataset: ADE20K, Cityscapes
### Notes
- The distance transform: 
  <img width="700" alt="1674005307603" src="https://user-images.githubusercontent.com/46414159/213058684-c2c2ac6d-2a4e-4d9e-9bfd-782659967032.png">
  The simplest Distance Transform, receives as input a binary image, (the pixels are either 0 or 1), and outputs a distance map. This distance map has the same dimensions of the input image and each pixel contains for example, the Euclidean distance, to the closest obstacle pixel (e.g. border pixel). https://medium.com/on-coding/euclidean-distance-transform-d37e06958216
