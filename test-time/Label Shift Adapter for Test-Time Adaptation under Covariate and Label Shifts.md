## [Label Shift Adapter for Test-Time Adaptation under Covariate and Label Shifts](https://arxiv.org/pdf/2308.08810v1.pdf)

ICCV 2023

### Introduction and background
<img width=300 alt="intro" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6ca0b99b-f6cc-4a1f-aff9-6dd036eeb44a">

- The previous method has temporal correlation, etc. Still, it does not cover the situation where the source domain data has a long-tailed label distribution, which can lead to bias in the source model. 
- Furthermore, we observed that training the source model on a long-tailed dataset with long-tailed recognition techniques, such as balanced softmax, is
insufficient to stabilize TTA algorithms.

Drawback:
Need to train the label shift adaptor before deployment (i.e., need customize source pertaining process)

### Method
<img width=700 alt="base" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4216a1fb-cdbb-403b-802d-78cde17a68ab">

- Label shift adaptor learn affine parameter $\gamma$ and $\beta$, as well as the weight difference of the classifier $\delta w$ and $\delta b$
- For the hidden feature h come from the feature extractor $F(\theta)$, we have:
  
  <img width=200 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ec317340-d574-45b6-94a5-06597c08c6b5">

- Note, above all happened during source pertaining.

  <img width=300 alt="loss1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/254cdc0d-ba81-42f0-ae0e-2573d007e9a1">

- During inference, use EMA to update test set label distribution:

  <img width=300 alt="loss2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2c07b689-f816-499a-a965-e6ecabe35ff2">

### Experiments

### Notes
