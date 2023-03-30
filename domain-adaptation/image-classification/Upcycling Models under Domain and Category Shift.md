## [Upcycling Models under Domain and Category Shift](https://arxiv.org/pdf/2303.07110.pdf)

CVPR2023

Main task: Universal Source-free DA for image classification

<img width=350, alt="1680131729167" src="https://user-images.githubusercontent.com/46414159/228688591-386ac639-66b7-4db0-8b6e-67cd5db3fcba.png">


### Introduction and background
- DNNs often generalize poorly to the unseen new domain under domain shift and category shift
- the access to source raw data is inefficient and may violate the increasingly stringent data privacy policies
- target data may come from a variety of scenarios

### Related work
- UDA
- Universal DA
- Source-free DA

### Method

<img width=750, alt="1680132644803" src="https://user-images.githubusercontent.com/46414159/228690449-f4c7c28d-3baf-4984-8bff-796cb6553eca.png">

- source-only label: $\overline{Y}_s$ ; target-only label: $\overline{Y}_t$
- PDA: partial-set DA $Y_t \subset Y_s$
- OSDA: open-set DA $Y_s \subset Y_t$
- OPDA: open-partial-set DA (both s and t have their private classes)
- source model: $f_s = h_s \circ g_s$, where $g_s$ is feature extractor and $h_s$ is the classifier

#### Algorithm
- only learn a target-specific feature module $g_t$ and keep the classifier $h_t = h_s$
- to identify "known" and "unknown", uses global one-vs-all clustering
- to avoid negative transfer, uses local k-NN clustering

#### One-vs-all Global Clustering (only for OSDA setting)
- Under source-free setting, it's hard to pseudo labeling when there is open-set or partial set setting
- one-vs-all global clustering pseudolabeling algorithm: For a particular “known” category $c \in C_s$, in order to decide whether a data sample belongs to the c-th category, we need to figure out what is and what is not the c-th category. 
- step 1: For a particular c-th category, aggregate the top-K $\sigma _c (f_t (x_t))$ scores represented instances along all target domain $D_t$ as positive $P_c$ , and the rest as negative $N_c$. 
- step 2: get the prototype representation of $P_c$ and $N_c$, note that the prototype of $N_c$ is calculated by kmeans (M=$C_t$)

  <img width=260, alt="1680140015551" src="https://user-images.githubusercontent.com/46414159/228705077-dda5cfde-3ea0-4b36-8bbb-fa3874c234a1.png">

- step 3: identify if $x_t$ belongs to c

  <img width=350, alt="1680140146124" src="https://user-images.githubusercontent.com/46414159/228705367-7702ca2a-ae5a-4255-82d5-702bf2e7672f.png">

- step 4: iterate the process to obtain plabels $\hat{y}_t$ for all known class $c \in C_s$

#### Confidence based Source-private Suppression (to make the algorithm applicable for PDA, OPDA setting)

- Key idea:  prevent those source-private categories from misleading pseudo-label assignments (considers the condition that source also has private labels)

- observation: compared with shared class, source-private class has lower confidence of top-k target sample

- uses source-private category suppression to modify above target assignment:

  <img width=400, alt="1680144631751" src="https://user-images.githubusercontent.com/46414159/228715745-bd8b4f30-b241-4e8e-bf9d-4a2a1d635c9c.png">

#### Silhouette Based Target Domain $C_t$ Estimation (deal with the situation that the number of target categories $C_t$ is not available)

  <img width=400, alt="1680145919571" src="https://user-images.githubusercontent.com/46414159/228718919-ea454b26-6d44-4fa2-aeec-f7a9f487711d.png">

- After that, we can have a rough number of how many classes exist in the target domain


#### Local Consensus Clustering (to deal with negative transfer causing by incorrect pseudo label assignments)

- step 1: maintain a memory bank $G_t$ of target features $g_t (x_t)$ and corresponding prediction score $\sigma (f_t (x_t))$

- step 2: apply the cosine similarity function to find the nearest neighbors $L^i$ of $x^i _t$ in the memory bank $G_t$.

  <img width=300, alt="1680146433495" src="https://user-images.githubusercontent.com/46414159/228720165-737dbb25-0a7d-4975-99fa-89594727427a.png">

- step 3: encourage minimizing the cross entropy loss between $x^i _t$ and the nearest neighbors $L^i$ to achieve the local semantic consensus clustering

  <img width=330, alt="1680146555188" src="https://user-images.githubusercontent.com/46414159/228720433-8d86d758-291a-4ee7-925a-a0ec612d7197.png">


#### Other details

- Objective: 
  <img width=400, alt="1680146778115" src="https://user-images.githubusercontent.com/46414159/228720916-d74341f5-cdc7-40e2-a8e3-d223e142a18f.png">

- inference:
  use entropy to determine if one class is known or unknown
  
  <img width=360, alt="1680146886450" src="https://user-images.githubusercontent.com/46414159/228721261-5d6dd9b2-9544-4027-b9d8-b7512d521505.png">
  
  <img width=350, alt="1680146941841" src="https://user-images.githubusercontent.com/46414159/228721308-c94b7739-7bba-4394-af8d-c8ddd6f9a23f.png">

$\omega$ is 0.55.

### Experiments
- dataset: Office-Home; Office-31; VisDA-C; DomainNet
- evaluation protocol: H-score
- empirical study:

<img width=750, alt="1680132087823" src="https://user-images.githubusercontent.com/46414159/228689332-e7df07c8-cfd8-4da5-828c-fa5ac6614e4b.png">

<img width=750, alt="1680132190357" src="https://user-images.githubusercontent.com/46414159/228689553-e53505ee-91a0-4f1d-bf7a-d79b522e739e.png">

<img width=750, alt="1680132247299" src="https://user-images.githubusercontent.com/46414159/228689694-ab72a877-cae9-44ab-b397-6ac8b3763413.png">

<img width=750, alt="1680148260313" src="https://user-images.githubusercontent.com/46414159/228724160-c5d377cd-bce1-44c2-be5c-541e4331710b.png">

<img width=750, alt="1680132429334" src="https://user-images.githubusercontent.com/46414159/228690057-e6837d30-e2e2-415e-9405-768a8f66a63f.png">

### Notes
The silhouette metric is a measure of how similar an object is to its own cluster compared to other clusters. It is calculated based on the distance between a sample and the neighboring clusters. It ranges from -1 to 1, where a score closer to 1 indicates that the sample is well matched to its own cluster and poorly matched to neighboring clusters.

The silhouette metric can be used to evaluate the quality of clustering results, where a higher silhouette score indicates better clustering. It can also be used to determine the optimal number of clusters by comparing the silhouette scores across different values of k. 
