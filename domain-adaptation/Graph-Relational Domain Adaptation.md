## [Graph-Relational Domain Adaptation](https://arxiv.org/abs/2202.03628)

ICLR2022

Ranking: ⭐ ⭐ ⭐ 

### Introduction and background
- Previous DA using uniform alignment that ignores topological structures among different domains (in practice the domains are often heterogeneous)
- A graph can be constructed to show the heterogeneity. the domains realize the nodes, and the adjacency between two domains can be captured by an edge
- Previous graph-based methods perform DA for each pair of neighboring domains separately. Due to the strict alignment between each domain pair, this method will still lead to uniform alignment so long as the graph is connected.
- While this paper argue that:
  - only enforce uniform alignment when the domain graph is a clique (i.e., every two domains are adjacent)
  - relax uniform alignment to adapt more ﬂexibly across domains according to any non-clique domain graph, thereby naturally incorporating information on the domain adjacency

### Method
#### Problem setting
- We have $N$ domains in total for unsupervised domain adaptation; discrete domain index $u \in \mathcal{U}=[N] \triangleq\{1, \ldots, N\}$ could be either source index $\mathcal{U}_s$ or target $\mathcal{U}_t$.
- The relationship between domains followed a domain graph $A=[A_{ij}]$
- In this setting, [data, label, domain index] for source & [data, domain index] for target are available.

#### Graph-relational Domain Adaptation (GRDA)
- Use a adversarial-based framework which has 3 component:
  - Encoder $E$: generate encoding from data, domain label and domain graph: $\mathbf{e}_l=E\left(\mathbf{x}_l, u_l, \mathbf{A}\right)$
  - Predictor $F$: makes prediction based on $\mathbf{e}_l$
  - <img width="350" alt="Screen Shot 2023-01-10 at 13 55 28" src="https://user-images.githubusercontent.com/46414159/211458402-4872b35e-9dc6-42ff-8998-52b3dc970b87.png">
  - Graph discriminator $D$: guides the encoding to adapt across graph-relational domains. It takes in a mini-batch of B encodings $\mathbf{e}_l \left(l \in [B]\right)$, and tries to reconstruct the domain graph $\mathbf{A}$.
  - By letting the encoder E play adversarially against the discriminator D, the graph-relational information of domains will be removed from the encoding $\mathbf{e}_l$ in order to make the discriminator D incapable of reconstructing the graph.

<img width="300" alt="Screen Shot 2023-01-10 at 14 32 07" src="https://user-images.githubusercontent.com/46414159/211462549-fdbc41ab-3f4c-4acb-adcf-7216a2496d5f.png">
#### Predictor
The predictor loss $L_f$ is the task loss on source domains
<img width="350" alt="Screen Shot 2023-01-10 at 14 33 32" src="https://user-images.githubusercontent.com/46414159/211462720-487f4aed-7e89-4a31-b716-4305030cc5ab.png">
$h_p$ is a predictor loss function.

#### Encoder and Node Embeddings

$z_{ul}$ is graph-informed domain embedding based on $u_l$ and $\mathcal{A}$, after get $z$, combined with $x_l$, we compute final encoding:   
<img width="300" alt="Screen Shot 2023-01-10 at 14 39 33" src="https://user-images.githubusercontent.com/46414159/211463416-e3784c61-d389-4fa2-b33e-6583e1c2e5ce.png">    
where $f(.,.)$ is trainable NN.   
Suppose the nodes indices $i$ and $j$ are sampled independently and identically from the marginal domain index distribution $p(u)$; the reconstruction loss is:   
<img width="500" alt="Screen Shot 2023-01-10 at 14 35 41" src="https://user-images.githubusercontent.com/46414159/211462962-ad5ed959-6939-415c-abfc-a7e95975534e.png">

where $\delta (x)$ is sigmoid function.

#### Graph Discriminator
<img width="900" alt="Screen Shot 2023-01-10 at 14 44 59" src="https://user-images.githubusercontent.com/46414159/211464089-0c58822a-b970-41b7-b70a-9b45b74513ea.png">


### Experiments
- datasets: DG-15; DG-60; TPT-48; CompCars
- exp:
  - <img width="400" alt="Screen Shot 2023-01-10 at 14 47 46" src="https://user-images.githubusercontent.com/46414159/211464408-f958d8b7-0518-44fd-9aec-aae5f4458359.png">
  - <img width="700" alt="Screen Shot 2023-01-10 at 14 48 19" src="https://user-images.githubusercontent.com/46414159/211464464-2e11c059-841a-4849-b2f0-4e1d43441fd6.png">
  - <img width="400" alt="Screen Shot 2023-01-10 at 14 48 51" src="https://user-images.githubusercontent.com/46414159/211464520-5579a989-3c0e-4a4b-bf8c-3d21aff90c9c.png">

