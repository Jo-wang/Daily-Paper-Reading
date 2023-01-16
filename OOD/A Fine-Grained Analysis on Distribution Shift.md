## [A Fine-Grained Analysis on Distribution Shift](https://arxiv.org/pdf/2110.11328.pdf)

ICLR2022 oral

Ranking: ⭐ ⭐ 🌟

### Introduction and background
- Can we define the important distribution shifts to be robust to and then systematically evaluate the robustness of different methods?

### Details
- Mainly focusing on:
  - 1. **Spurious correlation**: Attributes are correlated in training data but not testing data. (e.g., all cars in training data are red, while car and red are not related)
  - 2. **Low-data drift**: data has not been collected uniformly across different attributes
  - 3. **Unseen data shift**: (a special case of low-data drift) when a model, trained in one setting is expected to work in another, disjoint setting. E.g., a model trained to classify animals on images at certain times of day should generalise to other times of day.
  
- Conditions: 
  - **Label noise**: labellers may have disagreements and errors. So we sue $\hat{y}^i \sim c(y^i)$ to model this kind of corruption of label. $c$ is the corrupting function.
  - **Dataset size**: how performance degrades given fewer total samples (limit the total number of samples from $p_\text{train}$)

- Models
  - **Architecture choice**:ResNet18, ResNet50, ResNet101, ViT, and an MLP; with weighted resampling $p_\text{reweight}$ under $p_\text{train}$
  - **Heuristic data augmentation**: standard ImageNet augmentation, AugMix without JSD, RandAugment, and AutoAugment; approximate the true underlying generative model $p(x \| y^{1:K})$ in order to improve robustness.
  - **Learned data augmentation**: CYCLEGAN without SGDRO objective; approximate the true underlying generative model $p(x \| y^{1:K})$ by learning augmentations conditioned on the nuisance attribute
  - **Domain generalization**: IRM, DeepCORAL, domain MixUp, DANN, and SagNet; recover a representation $z$ that is independent of the attribute: $p(y_\alpha; z) = p(y^\alpha)p(z)$ to allow generalization over that attribute.
  - **Adaptive approaches**: JTT, BN-Adapt; modify $p_\text{reweight}$ dynamically.
  - **Representation learning**: $\beta$-VAE, pretraining on ImageNet; learn a robust representation of $z$ that describes the true prior.
  

### Experiments
- dataset: DSPRITES, MPI3D, SHAPES3D, SMALLNORB, CAMELYON17, IWILDCAM
- model selection: ResNet-18, ResNet-50; choose the best model according to the in-distribution validation set; In the unseen data shift setting for the CAMELYON17 and IWILDCAM, use the given out-of-distribution validation set.
- hyperparameter: sweep and 5 seeds

### Takeaways:
- While we can improve over ERM, no one method always performs best.
- Pretraining is a powerful tool across different shifts and datasets.
- Heuristic augmentation improves generalization if the augmentation describes an attribute.
- Learned data augmentation is effective across different conditions and distribution shifts. 
- Domain generalization algorithms offer limited performance improvement.
- The best algorithms may differ under the precise conditions.
- The precise attributes we consider directly impacts the results.

### Tips:
- Use, If heuristic augmentations approximate part of the true underlying generative model.
- If heuristic augmentations do not help, learn the augmentation.
- Use pretraining.
- More complex approaches lead to limited improvements.

### Notes
This is mainly a discussion about different types of distribution shift (with empirical study)
