## [Freesolo: Learning to segment objects without annotations](https://arxiv.org/abs/2202.12181)

CVPR2022

Ranking: :star: :star: :star: :star:

### Introduction and background

- Instance segmentation requires costly annotations such as bounding boxes and segmentation masks for learning.

- We propose a fully unsupervised learning method that learns class-agnostic instance segmentation without any annotations.

- Freesolo is a novel localization-aware pre-training framework

- it contains two major pillars: Free Mask and Self-supervised SOLO

### Method
<img width="750" alt="1675749015005" src="https://user-images.githubusercontent.com/46414159/217159667-f6ba0d81-fb8d-48f0-b9cd-024b2acef6a9.png">
#### Free Mask
<img width="350" alt="1675750532447" src="https://user-images.githubusercontent.com/46414159/217163506-71e94447-81a8-4055-975d-a228103d5789.png">
- Q is downsampled from feature I (it has different scales and we flatten and concat them together to get the final Q)
- K is I itself
- for each Q and K, compute the cosine similarity, then we can get the score map S $S_{ijq} = sim(Q_q, K_{ij})$, where $Q_q$ is $q^{th}$ query and ij is the position of key
- score maps then normalized as soft masks by shifting the score range to [0,1], and use threshold T to make it binary mask.
- sort the binary masks by maskness scores and use mask NMS to remove redundant masks.
- finally get coarse masks at this step

#### Self-supervised SOLO
<img width="350" alt="1675753645413" src="https://user-images.githubusercontent.com/46414159/217172434-19eae7bc-3684-41b7-aca9-9dadfc4bf862.png">

<img width="350" alt="1675753737108" src="https://user-images.githubusercontent.com/46414159/217172679-09a19575-bd4c-4c03-a344-f4707e200f0f.png">

- self-training with the initially trained instance segmenter to further improve accuracy. We input unlabeled images into the instance segmenter and collect their predicted object masks. The lowconfidence predictions are removed and the remaining ones are treated as a new set of coarse masks. We again train an instance segmenter with the unlabeled images and the new masks, using the loss function
- decouple the category branch to 2:
  - foreground/background binary classification (focal loss)
  - semantic embedding learning:
  <img width="350" alt="1675754634701" src="https://user-images.githubusercontent.com/46414159/217176354-03c33966-5fd0-471c-844d-f4e9b0eea9e3.png">

  
### Experiments
- dataset: MS COCO, PASCAL VOC

<img width="350" alt="1675754901091" src="https://user-images.githubusercontent.com/46414159/217178006-0219126b-e94e-4c80-ac2e-61f2a90df5ba.png">

<img width="350" alt="1675754965800" src="https://user-images.githubusercontent.com/46414159/217178400-742cdd6d-ae69-4936-ae90-8e150d6f995f.png">

### Ablation Study
<img width="700" alt="1675755053598" src="https://user-images.githubusercontent.com/46414159/217178990-84774aad-c8e6-46f8-918e-1827bdfe610e.png">

### Notes
