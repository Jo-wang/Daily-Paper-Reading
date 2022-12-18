
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
<img width="448" alt="Screen Shot 2022-12-18 at 14 21 02" src="https://user-images.githubusercontent.com/46414159/208281335-8f09814f-7f56-4c69-96c5-ee8ec16389ca.png">

- Given an image x, a binary mask m, the goal of inpainting function f is to synthesize a new image y with the masked regions filled: $y=f(x, m)$
- This paper propose MAE-VQGAN model.   
- Models the distribution $p_{\theta}(z_{i}|x, m)$, where $z_{i}$ is visual token from VQGAN vocabulary V that corresponds to the $i^{th}$ ViT patch.   
- The codebook in VQGAN is the fixed ImageNet pretrained codebook.    
- MAE-VQGAN assigns probabilities to visual tokens via a softmax layer, which is better suited for capturing ambiguities. During training, we obtain ground truth visual tokens by mapping the image to visual tokens indices using the VQGAN encoder. The model is trained using cross entropy loss.
- $\hat{z}$ is the predicted visual token: $\hat{z_{i}}=argmax p_{\theta}(z_{i}|x, m)$, then use VQGAN decoder $\hat{z} -> y$

#### Visual prompting

### Experiments
- Dataset: ﬁgures and infographics from computer vision articles available on Arxiv. Contain grids of images and their corresponding task results (e.g. images and their segmentation masks/stylized versions/edges, etc.).
- Predict randomly masked patches from ﬁgures given other patches from the same ﬁgure.

### Notes
- MAE (Masked Autoencoder): https://www.zhihu.com/question/498364155/answer/2240224120
- MAE implementation: https://zhuanlan.zhihu.com/p/439554945
- VQGAN: 详解VQGAN（一）| 结合离散化编码与Transformer的百万像素图像生成 - 卡卡猡特的文章 - 知乎
https://zhuanlan.zhihu.com/p/515214329
