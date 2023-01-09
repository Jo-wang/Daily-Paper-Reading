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
- :star: The baisc way of training is a student-teacher manner. Do backpropogate on student and EMA update the parameter to teacher. Do pseudo labeling and target test on teacher model.

- **Stochastic Label Mapping (SLM)**: deal with one(source)-to-many(target) e.g., person ➡️ {rider, pedestrian}   
  - map the source domain classes to the corresponding target label space   
  - $\widetilde{y}^{s(m,n)}=rand(c_{p}^t, c_{p+1}^t, \cdots, c_{p+q-1}^t)$, (m,n) is the (row, column) index.
  - Then use $L_{slm}=CE(F_{\theta}(x_s), \widetilde{y}^s)$ to learn the model, where $F_{\theta}$ is the student model.
- **Pseudo-Label based Relabeling (RL)**: 
  - inteead of using SLM in the latter stage, we use model prediction pseudo labeling (on teacher model) to relabel the source data with a defined threshold. 
  - $L_{rl}=CE(\widetilde{y}^s, F_{\theta}(x_s))$
- **Bilateral Mixed Sampling (BMS)**: aims to unify the consistent and inconsistent taxonomy classes and augment the few-shot supervision for the target domain
  - class-mixed sampling strategy from $x^s$ to $x^u$, and from $x^{t_{j}}$ to $x^u$
  -  The bilateral mixed sampling mask $m^s$ of $x^s$ is:
      <img width="260" alt="1673246914218" src="https://user-images.githubusercontent.com/46414159/211253788-fb188ba8-f1ea-451d-9fa6-d9ad1d9f1ed2.png">
    class $c_r$ is randomly selected from the available classes in $\widetilde{y}^s$.   
  
  - The augmented target sample and corresponding pseudo label are:  
      
    <img width="350" alt="1673247335217" src="https://user-images.githubusercontent.com/46414159/211254585-bb456d51-715b-467a-a320-e0330467975f.png">
    
- **Image level: Uncertainty-Rectified Contrastive Learning (UCT)**: CT :arrow_right: UCT

  - contrastive learning conducted on the augmented target domain image sample $\hat{x}^u$, and corresponding pseudo-label $\hat{y}^u$ in the BMS module
  - model $F_\theta$ can be split into encoder $\varepsilon_\theta$ and decoder $M_\theta$, so we have feature $\hat{v}^u$ 
  - pseudo-label based contrastive learning module loss: 
    <img width="450" alt="Screen Shot 2023-01-09 at 20 48 30" src="https://user-images.githubusercontent.com/46414159/211291066-2b84de4b-6214-40f6-82c5-cda73f33b666.png">
    where $P_v$ are positive samples. The positive samples in $P_v$ are the feature vectors whose corresponding pixels in $\hat{y}^u$ have the same class label as that of the corresponding pixel of v. The negative samples in $N_v$ are the feature vectors whose corresponding pixels in $\hat{y}^u$ have the different class label from that of the corresponding pixel of v.     
  - pseudo label may have wrong labels, to alleviate the incorrect guidance, they propose **UCT**.
  - use maximum prediction probability of $x^u$ as the uncertainty est. 
    $\hat{\mathbf{u}}^u=\max_c\mathcal{F}_{\theta^{\prime}}\left(\hat{\mathbf{x}}^u\right)$.
    Then the new loss: 
    <img width="400" alt="Screen Shot 2023-01-09 at 22 28 35" src="https://user-images.githubusercontent.com/46414159/211308078-9b548962-3068-464f-bf90-4ac61ec28368.png">

**Objective**:     
<img width="400" alt="Screen Shot 2023-01-09 at 22 33 48" src="https://user-images.githubusercontent.com/46414159/211308995-2bf9809d-dff2-4122-9a09-bdd86c3738b5.png">


### Experiments
- DeepLabv2-ResNet101
- UDA: Consistent Taxonomy: Synthia :arrow_right: Cityscapes. same label space   
<img width="800" alt="Screen Shot 2023-01-09 at 22 38 02" src="https://user-images.githubusercontent.com/46414159/211309775-d8238b52-0aa1-4090-94c5-3c46c62c6ab6.png">

- TACS: Open Taxonomy: Synthia :arrow_right: Cityscapes. 13 of Synthia classes are labeled, 6 of Cityscapes are few-shot labeled.    
<img width="800" alt="Screen Shot 2023-01-09 at 22 38 35" src="https://user-images.githubusercontent.com/46414159/211309899-fd3ee02a-887f-423d-97ee-a040b1e533b1.png">

- TACS: Coarse-to-Fine Taxonomy: GTA5 :arrow_right: Cityscapes. one-to-many; few-shot labeled on target.      
<img width="800" alt="Screen Shot 2023-01-09 at 22 41 02" src="https://user-images.githubusercontent.com/46414159/211310295-4b12fea6-5c4c-4d1b-a6fe-027e02e2db47.png">

- TACS: Implicitly-Overlapping Taxonomy: Synscapes :arrow_right: Cityscapes. many-to-many; few-shot labeled target.    
<img width="800" alt="Screen Shot 2023-01-09 at 22 43 43" src="https://user-images.githubusercontent.com/46414159/211310776-3cb47499-fe50-42ca-9fdb-d3c4c0d34ee8.png">

### Notes
