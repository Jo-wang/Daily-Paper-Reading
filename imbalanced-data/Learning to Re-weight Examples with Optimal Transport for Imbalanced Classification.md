## [Learning to Re-weight Examples with Optimal Transport for Imbalanced Classification](https://arxiv.org/pdf/2208.02951.pdf)
NeurIPS 2022

### Introduction and background
- Most real-world datasets are imbalanced, training model would be signiﬁcantly dominated by those majority classes
- The major challenge of imbalanced classification is essentially the mismatch between the imbalanced training dataset and the balanced test set.
- Previous methods of dealing with imbalanced data is re-weighting (in loss functions), including re-sampling, class-level or instance-level re-weighting, meta-learning, two-stage methods and post-hoc correction.
- L2RW set the weight as a learnable parameter with unbiased meta set, but the parameter is coupled with the to-be-learned classifier. The dependence of weights on classiﬁer at training stage may lead to inaccurate learning of the weights.
- Math:  
$D_{train}$: imbalanced training data  
$D_{meta}$: small balanced meta set
$f(x, \theta)$: model, parameterized by $\theta$

- Typical way of re-weighting is use $w$ to weight the loss for different classes and use meta set to learn this $w$. The classiﬁer has been proved to be the major concerning part in imbalanced issue.
- OT distance between $p$ and $q$:
<img width="911" alt="Screen Shot 2022-11-04 at 15 24 12" src="https://user-images.githubusercontent.com/46414159/199896486-a30591f5-9350-4c40-bc34-1a0054ee73a0.png">

- [More OT things](https://zhuanlan.zhihu.com/p/458312488)

### Method
#### Re-weighting Methods with OT
##### 1. Main Objective  
- Sample probability for imbalanced training data:
<img width="294" alt="Screen Shot 2022-11-04 at 16 08 05" src="https://user-images.githubusercontent.com/46414159/199903575-cf1c099d-d6c1-4832-839a-b3365b2e43a6.png">, where $w_{i}$ is the sample probability (i.e., the weight), we want to get $w$.

- Sample probability of balanced meta set:
<img width="243" alt="Screen Shot 2022-11-04 at 16 08 48" src="https://user-images.githubusercontent.com/46414159/199903660-d8dd23ee-c4dd-456a-adfa-813da4473e5b.png">, where $M$ is the number of meta samples.

- OT distance between $P(w)$ and $Q$:
<img width="447" alt="Screen Shot 2022-11-04 at 16 12 12" src="https://user-images.githubusercontent.com/46414159/199904069-91109e71-80a1-4110-9763-8c1e48e6a060.png">


##### 2. Cost Function
- Label-aware cost
<img width="227" alt="Screen Shot 2022-11-04 at 17 04 51" src="https://user-images.githubusercontent.com/46414159/199912222-01f964d4-33ad-43b5-a103-bf5d0c7a513b.png">, euclidean distance (0-1 matrix)

- Feature-aware cost
<img width="233" alt="Screen Shot 2022-11-04 at 17 05 12" src="https://user-images.githubusercontent.com/46414159/199912344-7040321a-67f6-408e-87e6-477c7ff0875a.png">, uses cosine distance

- Combined Cost
<img width="401" alt="Screen Shot 2022-11-04 at 17 05 28" src="https://user-images.githubusercontent.com/46414159/199912434-a7ae9aee-d831-4eeb-8522-1c8fb1b7ea37.png">, where $d^{ fea}=1-cosine(.,.)$ and $d^{ lab}$ is duclidean distance.

##### 3. Learn the Weight Vector
- Uses entropy regularized OT loss to learn the weight vector: 
<img width="800" alt="Screen Shot 2022-11-06 at 13 00 05" src="https://user-images.githubusercontent.com/46414159/200151898-84866ee7-c0a1-4119-8082-fb0c234aed6c.png">

#### Overall Algorithm and Implementation
- Stage 1 trains the model f(θ) by the standard cross-entropy loss on the imbalanced training set.
- Stage 2 aims to learn the weight vector w and meanwhile continue to update the model f(θ).

<img width="782" alt="Screen Shot 2022-11-06 at 13 25 08" src="https://user-images.githubusercontent.com/46414159/200152523-d5db5c34-0fe0-4340-8dd5-03fe713cfad1.png">

- Prototype-oriented OT loss (POT):  
Average all samples from each class in the meta set to achieve its prototype and propose a new Q distribution (meta set distribution) over K prototypes: <img width="350" alt="Screen Shot 2022-11-06 at 13 29 11" src="https://user-images.githubusercontent.com/46414159/200152628-056b5b8e-fb7b-426c-837b-cce7987eb1a8.png">


### Experiments  
*Mainly focusing on image classification*

<img width="300" alt="Screen Shot 2022-11-06 at 13 50 27" src="https://user-images.githubusercontent.com/46414159/200153249-7011efe1-3e58-4f0f-ac21-98b405cceccd.png">

### Notes
- This is a auto way to deal with imbalanced data problems, where the defination of "imbalance" is coming from the inconsistency of imbalanced training set and balanced test set. But if we want to directly use it, we need to construct a balanced meta set, which is impossible in semantic segmentation task.
