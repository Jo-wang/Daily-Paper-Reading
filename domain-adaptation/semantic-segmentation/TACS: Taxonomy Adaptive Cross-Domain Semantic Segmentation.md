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

### Method

### Experiments

### Notes
