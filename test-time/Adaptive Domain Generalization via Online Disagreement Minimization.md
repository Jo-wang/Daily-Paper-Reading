## [Adaptive Domain Generalization via Online Disagreement Minimization](https://arxiv.org/abs/2208.01996)

2022

### Introduction and background
- A recent study on large-scale benchmarks shows that most existing DG methods actually do not bring signiﬁcant beneﬁts compared with the naive Empirical Risk Minimization (ERM). 
- How to facilitate DG to further utilize target domain information?
- TTA
- we optimize the feature extractor to minimize the prediction disagreement among source classiﬁers and optimize the classiﬁers to maximize it. Consequently, the feature extractor becomes more invariant to domain changes, while the classiﬁers are more sensitive to distribution differences among different domains.
- During inference, source classiﬁers are frozen, and the feature extractor is adjusted to reduce the prediction disagreement among classiﬁers
  
### Method
#### Source pretraining
<img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5203c7ac-6e92-4c66-b8c9-d18dff6cdfae">

<img width=400 alt="af" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8983a20b-7190-47de-8ce5-b84f4dffab0d">

During source pertaining, we use adversarial training when learning from labeled source data; specifically, we minimize the DS on feature extractor $g$ and maximize it on classifiers $h$ by gradient reversal layer (GRL) so that the DS objective could further be written as: 

<img width=350 alt="adf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8467131a-e52c-4866-ab63-cb0dfe7cc63d">

where $n^d$ is the domain index.

Then the final objective of source pretraining is: 
     
<img width=350 alt="addf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8220b1ef-6e0d-4061-9d44-cf0542e3d0c5">

where $\mathcal{\text{ERM}}$ is: 

<img width=200 alt="adffdf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f3966788-2ef2-458e-9cc9-ef23af537b61">

#### Test data adaptation

<img width=400 alt="adddf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e7e1f46a-8b88-4482-8d2d-50940b9db89b">

### Experiments
- Dataset: VLCS, PACS, OfficeHome, and TerraIncognita
- R-50
- batch size to 64
- <img width=600 alt="adddf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8459568b-0cde-4659-9b67-0bee09d388a7">

### Notes
