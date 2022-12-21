## [Pixel-by-Pixel Cross-Domain Alignment for Few-Shot Semantic Segmentation](https://openaccess.thecvf.com/content/WACV2022/papers/Tavera_Pixel-by-Pixel_Cross-Domain_Alignment_for_Few-Shot_Semantic_Segmentation_WACV_2022_paper.pdf)

WACV2022

Ranking: 3

### Introduction and background
- intrinsic imbalance between source and target data 
- Adversarial learning previously focusing on global-level 
- xxx

### Method
#### PixAdv

- Since global-level adversarial learning may mainly focusing on the well represented classes, this paper propose a pixel-wise discriminator to predict if one pixel come from source or target. 

![1671598938713](https://user-images.githubusercontent.com/46414159/208825554-bc077f1b-2e65-4e56-8236-7d602145d362.png)
- But this didn't consider class imbalance problem and may lead to negative transfer effect.
- So, this paper propose PixAdv loss that align each pixel according to its importance.
![1671599222229](https://user-images.githubusercontent.com/46414159/208826105-f1cd6888-9a57-4491-a03c-f1042473ba06.png)
where S is: ![1671599257668](https://user-images.githubusercontent.com/46414159/208826158-39dae7a8-43e1-4af2-92e9-d5d1d2cf4d03.png)

higher $S_{i}$ means the network misrepresent the pixel i.

B is the imbalance of the pixels: ![1671599324675](https://user-images.githubusercontent.com/46414159/208826274-af7e7c3f-05c8-4638-ad97-6fe496247791.png)

B approaches to 1 means a misrepresented class and 0 is a well-represented class.

**Note:**  the terms S and B aren’t used in backpropagation, but rather as a pixel-by-pixel map to modulate
the adversarial loss.

- The overall segmentation network training loss function is: source_seg + target_seg + $\lambda$ PixAdv

#### Sample selection
simultaneously train a global image-wise domain discriminator $D_{g}$:
![1671603216535](https://user-images.githubusercontent.com/46414159/208834521-ab5b213f-91b7-49c8-ac5b-906c1f768318.png)
distinguish source from target and to capture both semantic and visual domain information.
Also use this to avoid bad source alignment.

#### Fine-Tuning and Knowledge Distillation

### Experiments
- some few-shot knowledge during validation:
  - N-way-K-Shot-classification: N stands for the number of classes, and K for the number of samples from each class to train on.
- dataset:
- 
### Notes
- Few-shot learning: https://neptune.ai/blog/understanding-few-shot-learning-in-computer-vision
