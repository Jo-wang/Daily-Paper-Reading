## [NOTE: Robust Continual Test-time Adaptation Against Temporal Correlation](https://arxiv.org/abs/2208.05117)

NeurIPS2022

Code: https://github.com/TaesikGong/NOTE

**Main Task:** present a new test-time adaptation scheme that is robust against non-i.i.d.
test data streams (with the time t changes)

### Introduction and background
- performance degrades under distributional shifts between the training data and test data
- previous work assume ($x_t, y_t$) i.i.d. drawn from $P_T (x,y)$
- However, the distribution of online test samples often changes across the time axis, i.e., ($x_t, y_t$) ∼ $P_T (x,y|t)$ in many applications

<img width=350 alt="1680673077780" src="https://user-images.githubusercontent.com/46414159/229990392-28dad764-6ae9-4f56-9949-38542ce6e07c.png">

- the existing model might be biased towards these imbalanced samples under the temporally correlated test streams

### Method

### Experiments

### Notes
