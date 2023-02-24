## [LEEP: A new measure to evaluate transferability of learned representations](link)

ICML2020

Ranking: 

### Introduction and background
- This paper LEEP, only need single forward pass
- Tt is the average log-likelihood of the expected empirical predictor
- LEEP does not make any assumption on the source and target input samples, except that they have the same size.

### Method
- **step 1: **compute dummy label distribution of the inputs in the target set $D$
- **step 2: **compute the empirical conditional distribution $\hat{P}(y \| z)$ of the target label $y$ given the source label $Z$
Since $\hat{P}(y \| z)=\hat{P}(y, z)/ P(Z)$, we need joint distribution first:

![image](https://user-images.githubusercontent.com/46414159/221101063-5995839b-62fb-46f6-a6a1-5e7b8bda68df.png)

where θ is the probability of the label z according to the categorical distribution θ(xi)

then:

![image](https://user-images.githubusercontent.com/46414159/221101509-5a701061-56ef-4015-8e5e-204d213f3407.png)

- **step 3: Compute LEEP using $\theta (x)$ and $\hat{P}(y|z)$

### Experiments

### Notes
