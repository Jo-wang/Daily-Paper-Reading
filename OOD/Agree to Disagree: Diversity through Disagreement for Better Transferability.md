
## [Agree to Disagree: Diversity through Disagreement for Better Transferability](https://openreview.net/forum?id=K7CbYQbyYhY)

ICLR2023 TOP 5%

Ranking:

### Introduction and background
D-BAT is a novel algorithm that trains an **ensemble** of models that have different predictive features. The algorithm encourages the models to **agree** on the training data (source distribution) but **disagree** on the OOD data (out-of-distribution data). This way, the models can learn diverse and robust representations that can transfer better to new domains or tasks.

D-BAT is based on a generalized notion of **mutual information** between models and data distributions. It uses a gradient-based method to optimize a diversity-inducing regularizer that measures the discrepancy between models. D-BAT can be applied to any model architecture and task that involves supervised learning.


### Method

D-BAT enforces agreement and disagreement among the models by using a novel loss function that combines two terms: a **discrepancy term** and an **agreement term**.

The discrepancy term encourages the models to disagree on OOD data by maximizing their pairwise distance in output space. The paper defines different types of discrepancy measures, such as KL-divergence, Wasserstein distance, and generalized discrepancy.

The agreement term encourages the models to agree on training data by minimizing their pairwise distance in output space. The paper uses cross-entropy as the agreement measure.

The final loss function is a weighted sum of these two terms, where the weight is determined by a binary classifier that predicts whether a given sample is OOD or not.


### Experiments

### Notes
