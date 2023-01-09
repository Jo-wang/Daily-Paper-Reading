## [TACS: Taxonomy Adaptive Cross-Domain Semantic Segmentation](https://arxiv.org/abs/2109.04813)

ECCV2021

Ranking: :star: :star: :star:

### Introduction and background
- Conventional methods for DA-seg typically focus on the image level domain gap
- <img width="600" alt="1673225109054" src="https://user-images.githubusercontent.com/46414159/211227058-5d99fcef-2d58-404a-9755-de8a2c8c71a3.png">
- this holds an assumption of having consistent taxonomies between source and target domains
- motivate us to consider the label level domain gap problem
- recent open/universal/class-incremental domain adaptation:
  - only took image classification as test-bed
  - only focused on unseen classes in the target domain
- 💥This paper explore the label level domain gap problem in 3 types:
  - Open taxonomy: some classes appear in the target domain, but are unlabeled or unseen in the source domain
  - Coarse-to-fine taxonomy: some classes in the source domain are split into several sub-classes in the target domain
  - Implicitly-overlapping taxonomy: for a certain class in the source domain, one or more of its sub-classes are merged into other classes in the target domain.
-  This paper proposes taxonomy adaptive cross-domain semantic segmentation (TACS)

#### Problem Statement
- source domain $D_{s}$, target labeled $D_{t}$ and target unlabeled $D_{u}$ 
- source & target sample distribution $P_{S}$ and $P_{T}$, $P_{S} \neq P_{T}$
- the label set space of $D_{s}$ and ${D_{u}, D_{t}}$ are given by $C_{s}$ and $C_{t}$, $C_{s} \neq C_{t}$
- the inconsistent taxonomy subsets of $C_{s}$, $C_{t}$ are denoted as $\bar{C_{s}}$ and $\bar{C_{t}}$
- the goal is train the model on $D_{s}$ $D_{u}, D_{t}$, evaluate on target domain data in the label sets space $C_{t}$

#### Taxonomy
- open taxonomy: new classes, unseen or unlabeled in the source domain, appear in the target domain
  $\exists \mathbf{c}_j^t \in \mathcal{C}_t$ such that $\mathbf{c}_i^s \cap \mathbf{c}_j^t=\varnothing, \forall \mathbf{c}_i^s \in \mathcal{C}_s$
- coarse-to-fine taxonomy: target domain has a finer taxonomy where source classes have been split into two or more target classes   
  <img width="520" alt="img1" src="https://user-images.githubusercontent.com/46414159/211229841-70d8f31e-fd35-46de-bb68-8fcffcf2c971.png">
- implicitly overlapping taxonomy: a class in the target domain has a common part with the class in the source domain, but also owns the
private part.   
  <img width="600" alt="img2" src="https://user-images.githubusercontent.com/46414159/211230086-bd360e85-c23a-4192-92ce-6c53c11aca48.png">
#### Few-shot/partially Labeled
- if $n^t \ll n^u$, few-shot
- if $n^t \centernot\ll n^u$, partically labeled

### Method
<img width="700" alt="1673229781719" src="https://user-images.githubusercontent.com/46414159/211230850-96756066-cb7d-4ac5-9306-c1db8899b59e.png">

- 

### Experiments

### Notes
