
## [Parameter-free Online Test-time Adaptation](https://arxiv.org/abs/2201.05718)

CVPR2022

### Introduction and background
- Existing test-time adaptation methods such as TENT and SHOT may not be effective for all scenarios because they do not explicitly study how their approach works across training strategies and architectures.
- The type of model being adapted is a variable that strongly affects the effectiveness of both TENT and SHOT.
- Additionally, these methods may over-adapt the model parameters, leading to poor performance or even catastrophic performance degradation.
- **In this paper**, LAME runs efficiently while requiring less memory than NAMs.
- It provides a correction to the output probabilities.
- This setting relaxes the original domain shift, allowing hierarchical labels to appear (especially sub-classes) in the test set.

### Method
- Define a latent assignment vector $\tilde{\mathbf{Z}}_i$, we want to approximate the true distribution $p(z \mid \mathbf{x})$ by maximize the log likelihood:
  <img width=250 alt="image" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6cddd1b2-f171-4e5f-833f-3ccb297b1eb1">
- to prevent over-confident assignments, we consider a negative-entropy regularization that discourages one-hot assignements for $\tilde{\mathbf{Z}}$
- So that we have: <img width=250 alt="image1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b064dcf4-695d-47be-87df-711a1841a03f">
- But we cannot access p as p is the test distribution, in the contrast, we can access q (source distribution)
- Add Laplacian regularization to encourage neighbouring points in the feature space to have consistent latent assignments.

  <img width=250 alt="image2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5119be55-62a7-44e0-a8ba-1dc51fe3cf1f">
  
  where the first term is the log likelihood for source distribution q, and the second term if the regularization. But this regularization is not convex, so this paper use concave-convex proceduce:
  
  <img width=200 alt="image3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5615ac1a-9a88-48ac-92bf-43dc9929c3f4">

### Experiments
- Backbone: RN-18, RN-50, RN-101, EfficientNet (EN-B4), ViT-B
- Pretrained dataset: trained on the standard ImageNet ILSVRC-12 training set, except for ViT-B which uses an additional ImageNet-21k pre-training step.
- Validation for hyperparameter search: original validation set of ImageNet; ImageNet-C-Val; ImageNet-C16
- Testing set: i.i.d. case: ImageNet-C-Test; ImageNet-V2. Non-i.i.d. case: ImageNet-V2; ImageNet-VID; LaSOT subset from TAO

### Note
- only have the result over all test set (avg), have no individual one
