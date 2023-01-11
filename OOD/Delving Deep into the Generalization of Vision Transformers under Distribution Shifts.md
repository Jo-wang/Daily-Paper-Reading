## [Delving Deep into the Generalization of Vision Transformers under Distribution Shifts](https://arxiv.org/abs/2106.07617)

CVPR2022

Ranking: ⭐ ⭐ ⭐ ⭐

### Introduction and background
- transformer has made remarkable achievements
- the generalization ability of Vision Transformers (ViTs) is still less understood
- out-of-distribution (OOD) generalization is a highly desirable capability of machine learning models
- Recent works indicate current CNN architectures generalize poorly on various distribution shifts (DS)
- taxonomy of DS into four conceptual groups: **background shifts, corruption shifts, texture shifts, and style shifts**.

- Some conclusions:
  - ViTs learn weaker biases on backgrounds and textures, but stronger inductive biases towards shapes and structures, which is more consistent with human cognitive traits. So we can think ViT has better generalization than CNNs.
  - Large scale ⬆️ OOD generalization ⬆️
  - ViTs trained with larger patch size deal with texture shifts better, yet are inferior in other cases.
  
### Method
⭐ we design GeneralizationEnhanced ViTs (GE-ViTs) from the perspectives of adversarial training, information theory and self-supervised learning. 
- Models:
  - Vision Transformer: DeiT; also utilize the data-efficient training scheme to train ViT-L/16 and ViT-B/32 and rename them DeiTL/16 and DeiT-B/32.
  - Big Transfer: build on ResNet-V2 models. BiT-S-R50X1 based on a ResNet-50 backbone; also train a version using the identical data
augmentation strategy from DeiTs for comparison, name them BiT and $\text{BiT}_{da}$.

- **Generalization-Enhanced ViTs**       
  <img width="300" alt="1673417776332" src="https://user-images.githubusercontent.com/46414159/211731612-7033cf96-f84a-4a47-9385-ef257696970e.png">

  - 🥇Adversarial Learning: use domain discriminator to promote the backbone to produce domain-confused features by adversarial training. It has one shared feature encoder $F$, a label predictor $C$ and a domain classifier $D$. Follows a very typical adversarial learning manner.      
    <img width="300" alt="1673417497763" src="https://user-images.githubusercontent.com/46414159/211730823-bb778459-806c-4cd9-829b-68aa47c5dd1f.png">
    
  - 🥈Minimax Entropy     
    <img  width="300" alt="1673417812382" src="https://user-images.githubusercontent.com/46414159/211731719-77ea073c-2aa6-4e11-9d5f-be409016cbde.png">    
    a cosine similarity based classifier $C$ aims to produce the class prototype, where $C$ contains a weight vector $W=[w_1, w_2, \cdots , w_{n_c}]$, $n_c$ is total number of classes. $C$ takes normailzed $F(x)$ as input and output $\frac{1}{T} \frac{\mathrm{W}^{\mathrm{T}} F(\mathrm{x})}{\|F(\mathrm{x})\|}$ , to minimize the distance between the **class prototypes** and **neighboring unlabeled target samples**, thus extracting discriminative target features.
    Prototype are oved towards the target by max the entropy $L_E$ of unlabeled samples and 
    feature extractor aims to min the entropy to make them better clustered around the prototype.
    <img width="300" alt="1673418770654" src="https://user-images.githubusercontent.com/46414159/211734635-502d2820-f6b3-43e5-86a6-96036e6b8123.png">

  - 🥉Self-supervised Learning             
    <img width="500" alt="1673417856755" src="https://user-images.githubusercontent.com/46414159/211731828-db905414-910f-4a02-a816-154e26d1db16.png">      
    $V_s$ and $V_t$ are maintained to store feature vectors of every sample from source and target.
    in-domain prototypical self-supervision loss:      
    <img width="300" alt="IS" src="https://user-images.githubusercontent.com/46414159/211738004-ac4b7f7e-56c4-426b-a717-9de959947bab.png">        
    where $c_s$ and $c_t$ return class index.        
    $P_{i,j}^S=\frac{\exp \left(\mu_j^s \cdot f_i^s / \phi\right)}{\sum \exp \left(\mu_r^s \cdot f_i^s / \phi\right)}$
    
    since a network is desired to have highconfident and diversified predictions, an objective is set for maximizing the mutual information between the input image and the network prediction: $L_{MIM}=E_X [H(p(y \mid x; \theta))] - H(E_{x \in {D_s \cup D_t}}[p(y\mid x; \theta)])$

The final objective is:        
<img width="400" alt="img2" src="https://user-images.githubusercontent.com/46414159/211742456-5d20c30b-7126-4572-8201-bf10bd9e92f8.png">

where $L_{CLS}$ is source CE loss.

### Experiments
- Background shift     
  <img width="700" alt="1673422033511" src="https://user-images.githubusercontent.com/46414159/211743606-6c6a38b4-8c43-4203-be67-64903be64cc0.png">

  - 相对于CNN模型，ViT表现出了更少的背景信息偏好。
  - ViT越大，越会将更多注意力放在前景上，从而提取更加和背景无关的表征。

- Corruption Shift     
  <img width="700" alt="1673422141420" src="https://user-images.githubusercontent.com/46414159/211744139-f849b717-2819-4e45-8326-b132ae62def7.png">

  - ViT相较于CNN应对corruption shift更好，且ViT在此情况下的泛化性能随模型尺寸提升而提高。
  - ViT面对添加局部噪声图像的泛化能力部分受益于多样化的数据扩充，但其架构带来的增益不能被忽略。
  - ViT训练过程中使用的patch尺寸并不会影响模型在IID和OOD数据上的差距，而是影响模型在IID数据上的泛化能力。

- Texture Shift       
  <img width="700" alt="1673422221537" src="https://user-images.githubusercontent.com/46414159/211744342-e766f9fd-0f4e-4278-8c56-329dbbaecdca.png">      
  - ViT对于形状信息更强的偏好致使其在texture shift数据下表现得更好，同时这种对于形状的偏好与模型尺寸呈现正相关关系。
  - 使用更大patch尺寸进行训练的 ViT有更强的形状信息偏好，从而局部的纹理信息的依赖更小。

- Style Shift     
  <img width="650" alt="1673422339534" src="https://user-images.githubusercontent.com/46414159/211744671-25185cdd-bd26-48a6-9f24-06f6b0ef6c28.png">      
  - ViT在style shift下的IID/OOD generalization gap表现具有多样性。

  <img width="650" alt="1673422445830" src="https://user-images.githubusercontent.com/46414159/211744987-44ab000a-eae0-4c57-bf3f-c019a4913ee1.png">       
  - ViT表现出了更强的对结构信息的偏好。
  <img width="650" alt="1673422518530" src="https://user-images.githubusercontent.com/46414159/211745196-3eb4de35-ca61-4d2e-9702-c0d4a544ba49.png">
  - ViT在不同层内逐渐消除不同级别语义的DS。

#### Generalization     
<img width="700" alt="imgg" src="https://user-images.githubusercontent.com/46414159/211745457-ec825a0a-ecc9-4a48-9fc9-c42d31a9b3bd.png">

### Notes


