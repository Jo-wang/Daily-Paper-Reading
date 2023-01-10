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

#### Predictor
#### Encoder and Node Embeddings
#### Graph Discriminator

### Experiments

### Notes
