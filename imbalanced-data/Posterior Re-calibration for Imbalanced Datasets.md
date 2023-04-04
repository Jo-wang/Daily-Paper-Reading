## [Posterior Re-calibration for Imbalanced Datasets](https://arxiv.org/pdf/2010.11820.pdf)

NeurIPS2020

**Main idea:** 

### Introduction and background
- it is important to study robust algorithms that can perform well with such imbalanced datasets and unseen situations during testing (label prior shift or non-semantic likelihood shift)
- This paper focusing on label prior shift
- Previous methods do not allow for a flexibly trade-off between precision and recall across the classes, and require re-training to target a testing label distribution.
- This method does not require re-training the original imbalanced classifiers
- Combining with existing methods, this method can deal with non-semantic likelihood shift (e.g., lighting, weather change)

### Method
#### Background
- **label prior shift:**  the prior (label) distribution changing between training and testing, i.e, $P_s(Y) \neq P_t(Y)$; this paper focus on the case where the training distributions have varying degrees of imbalance (e.g. long-tailed) and the testing distribution shifts (e.g. is uniformly distributed).

- **non-semantic likelihood shift:** shift without introducing new semantic labels such as sensor degradations, changes in lighting, or presentation of the same categories in a different modality, i.e. $f_s(X \mid Y) \neq f_t(X \mid Y)$

<img width=700 alt="1680592166128" src="https://user-images.githubusercontent.com/46414159/229715219-44c80950-6438-4eef-8903-d0689f629b5d.png">

#### Imbalance Calibration (IC) with Prior Rebalancing

#### Confidence Calibration with Likelihood Flattening

### Experiments

### Notes
UNO: Uncertainty-aware Noisy-Or Multimodal Fusion for Unanticipated Input Degradation
