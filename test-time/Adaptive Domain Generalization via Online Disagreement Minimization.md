## [Adaptive Domain Generalization via Online Disagreement Minimization](https://arxiv.org/abs/2208.01996)

2022

### Introduction and background
- A recent study on large-scale benchmarks shows that most existing DG methods actually do not bring signiﬁcant beneﬁts compared with the naive Empirical Risk Minimization (ERM). 
- How to facilitate DG to further utilize target domain information?
- TTA
- we optimize the feature extractor to minimize the prediction disagreement among source classiﬁers and optimize the classiﬁers to maximize it. Consequently, the feature extractor becomes more invariant to domain changes, while the classiﬁers are more sensitive to distribution differences among different domains.
- During inference, source classiﬁers are frozen, and the feature extractor is adjusted to reduce the prediction disagreement among classiﬁers
  
### Method
![Screen Shot 2023-06-26 at 23 14 32](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5203c7ac-6e92-4c66-b8c9-d18dff6cdfae)
![Screen Shot 2023-06-26 at 23 15 13](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e7e1f46a-8b88-4482-8d2d-50940b9db89b)

### Experiments

### Notes
