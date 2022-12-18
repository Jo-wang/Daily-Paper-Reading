
## [Visual Prompting via Image Inpainting](https://arxiv.org/pdf/2209.00647.pdf)

NeurIPS2022

Ranking: 4      
<img width="700" alt="Screen Shot 2022-12-16 at 17 45 13" src="https://user-images.githubusercontent.com/46414159/208048802-a234c346-72f7-4f0d-808c-0446d73172d9.png">

### Introduction and background
- Overfitting problem in conventional DL with small dataset
- self-supervision need to fine-tune to adapt to downstream task
- If possible, how to avoid fine-tune?

### Method
#### Proposed inpainting model
- Given an image x, a binary mask m, the goal of inpainting function f is to synthesize a new image y with the masked regions filled: $y=f(x, m)$
- This paper propose MAE-VQGAN model.
#### Visual prompting
### Experiments
- Dataset: ﬁgures and infographics from computer vision articles available on Arxiv. Contain grids of images and their corresponding task results (e.g. images and their segmentation masks/stylized versions/edges, etc.).
- Predict randomly masked patches from ﬁgures given other patches from the same ﬁgure.

### Notes
