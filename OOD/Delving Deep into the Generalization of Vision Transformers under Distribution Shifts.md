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


### Notes


