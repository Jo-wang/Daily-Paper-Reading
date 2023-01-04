## [Uncertainty Modeling for Out-of-Distribution Generalization](https://arxiv.org/abs/2202.03958)

ICLR2022

Ranking: :star: :star: :star: :star:

### Introduction and background
- Previous work say feature statistics (mean and standard deviation) **carry informative domain characteristics** of the training data.
- :star: To define domain characteristic: the information that is more specific to the individual domains but less relevant to the task objectives.
- Consequently, domains with different data distributions generally have inconsistent feature statistics 
- Uncertain statistics shifts: 
![1672794785819](https://user-images.githubusercontent.com/46414159/210466607-01cdff7b-b595-4575-b0f6-cdf065effb9c.png)
- Previous methods are mainly linear manipulation on pairwise samples to generate new feature statistics. (sub-optimal)
- In this paper, to improve the generalization ability, they are trying to properly modeling **Domain Shifts with Uncertainty (DSU)**, i.e., characterizing the feature statistics as uncertain distributions.

### Method
- Preliminaries: intermediate feature $x$, channel-wise mean $\mu$, and std $\sigma$
![1672795784429](https://user-images.githubusercontent.com/46414159/210467966-7767b4bf-c712-4400-96fd-4a9679c381e1.png)

### Experiments

### Notes
