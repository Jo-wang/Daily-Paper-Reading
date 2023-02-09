## [Dirichlet-based Uncertainty Calibration for Active Domain Adaptation](https://openreview.net/forum?id=4WM4cy42B81)

ICLR2023

Ranking: ⭐ ⭐ ⭐ 

### Introduction and background
- traditional AL methods based on either predictive uncertainty or diversity are less effective for active DA, since they do not consider the domain shift
- The predictive uncertainty they used is still mainly based on the prediction of deterministic models, which is a point estimate and can easily be miscalibrated on data with distribution shift 

  <img width="400" alt="1675857307076" src="https://user-images.githubusercontent.com/46414159/217522970-96b1c817-e9b0-4c1f-b005-df9ee6e27a78.png">
  
- Observation: traditional DNNs tends to have a very low entropy (high confidence) on the target unlabeled data and leads to miscalibration
  
- Based on above, this paper propose Dirichlet-based Uncertainty Calibration (DUC) for active DA. (based on another work: Dirichlet-based evidential deep learning (EDL) The resulting benefit is that the miscalibration of
unilateral prediction can be mitigated by considering all possible predictions.)

  <img width="450" alt="1675860068685" src="https://user-images.githubusercontent.com/46414159/217532491-5e76f2b6-a347-4ba1-808e-9a4a76e594ad.png">
  
- the real-world style of the first target image obviously differs from source domain and presents a broader spread on the probability simplex, i.e., higher distribution uncertainty. This uncertainty enables us to measure the targetness without introducing the domain discriminator or clustering, greatly saving computation costs. While the second target image provides different information mainly from the aspect of discriminability, with the Dirichlet distribution concentrated around the center of the
simplex.

### Method
#### Problem Formulation
- Source $S$, target labeled $T^l$, and target unlabeled $T^u$
- Total budget $B$ for active learning setting

#### DIRICHLET-BASED EVIDENTIAL MODEL
- instead of using softmax to obtain the highest value as prediction, Dirichlet-based evidential model treats the prediction of class probability vector ρ as the generation of subjective opinions (random variables)
- a Dirichlet distribution, the conjugate prior distribution of the multinomial distribution, is placed over ρ to represent the probability density of each possible ρ. Given sample $x_i$, the PDF is:
  <img width="750" alt="1675910172752" src="https://user-images.githubusercontent.com/46414159/217703240-f44a7028-3c86-4614-bb56-0e661c569cfa.png">
- the parameters $\alpha _i$ of Dirichlet distribution is closely linked with the evidences collected to support the subjective opinion for sample $x_i$, via the equation $e_i = a_i -1$ where $e_i$ is the evidence vector.
- Connection with softmax-based DNNs: 
  <img width="750" alt="1675910456695" src="https://user-images.githubusercontent.com/46414159/217703847-e1ee053e-30b8-4678-989c-b5aaa04b1b42.png">

#### SELECTION STRATEGY WITH AWARENESS OF UNCERTAINTY ORIGINS
- use the uncertainty resulting from the lack of evidences, called **distribution uncertainty**, to measure the targetness.
  <img width="750" alt="1675910638083" src="https://user-images.githubusercontent.com/46414159/217704267-bfc6814b-00b5-41e3-8212-e619d0801b80.png">
  <img width="750" alt="1675910746077" src="https://user-images.githubusercontent.com/46414159/217704551-2182f05b-303c-4f38-91dc-88723a395b36.png">
  
- **Data uncertainty**:   
  <img width="750" alt="1675910856657" src="https://user-images.githubusercontent.com/46414159/217704868-e6b6d9b9-f45f-443b-b870-a0f45bfe53f6.png">
  
  <img width="750" alt="1675911025759" src="https://user-images.githubusercontent.com/46414159/217705308-afd93b42-02dc-4345-bdb6-d1b2790bf679.png">

- **target selection**: In each active selection step, we select samples in two rounds. In the first round, top κb target samples with highest $U_\text{dis}$ are selected. Then according to data uncertainty $U_\text{data}$, we choose the top b target samples from the candidates in the first round to query labels. 

#### MODEL LEARNING
<img width="800" alt="1675911642166" src="https://user-images.githubusercontent.com/46414159/217706902-cfa4b649-7095-4cda-ab63-d083b9b0b47a.png">


### Experiments
- dataset: miniDomainNet, Office-home, GTA5 - Cityscapes; Synthia - Cityscapes

![1675911873486](https://user-images.githubusercontent.com/46414159/217707421-a28e8e63-3dfc-4ae6-9bf9-aa463807a9fc.png)

![1675911898753](https://user-images.githubusercontent.com/46414159/217707473-0f76aab5-ba17-459f-9ee4-34dda0e456c4.png)

### Ablation Study
<img width="350" alt="1675911984631" src="https://user-images.githubusercontent.com/46414159/217707648-4edd59db-09d4-4cba-b5db-08ef95e50b0d.png">

<img width="350" alt="1675911924488" src="https://user-images.githubusercontent.com/46414159/217707527-2699091c-c0cf-4faf-b727-ea056d0706ef.png">

### Notes
- Based on Subjective Logic, the Dirichlet-based evidential model intrinsically captures different origins of uncertainty: the lack of evidences and the conflict of evidences
  - the distribution uncertainty is to express the lack of evidences, which mainly arises from the distribution mismatch, i.e., the model is unfamiliar with the data and lacks knowledge about it
  - the conflict of evidences is expressed as the data uncertainty, which comes from the natural data complexity, e.g., low discriminability. 
![1675912064597](https://user-images.githubusercontent.com/46414159/217707787-48f6f103-931e-475f-8236-7ab349a67a63.png)
