
## [MECTA: Memory-Economic Continual Test-Time Model Adaptation](https://openreview.net/pdf?id=N92hjSf5NNh)

ICLR2023 Poster

### Introduction and background
- Previous TTA such as Tent gains OOD performance via online optimization which is accompained by large memory consumption and are prohibitive in many real-world Continual Test-time Adaptation (CTA) applications. 
- To overcome this challenge, we need to improve the acc via reduce the memory cost.
- Mainly ofcusing on cache of BP (i.e., batch size, channel and layer number)

### Method
<img width=700 alt="1685865614571" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cbc207b6-46cc-4886-a0bd-e4efe2063fa2">

- **The fact**: assume we only update the affine parameter of batch norm layer, th3e cache consumption is maintained for each BN of its latent representations (B * C * W * H) for calculating the gradient.
- Intuitively, we can think about reduce B, C and L (batch size, channel and number of layers)
- **Reduce B**: use EMA to update the statistic parameters, while the decaying factor $\beta$ is adaptable and defined as: 
  <img width=550 alt="1685925548692" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6cc57c8e-acf9-4abb-9433-8971d4eb8728">
  
  with the intuition that if the test data from single distribution, we need a small $\beta$ to remember the previous steps' info and if the test coming from different distribution, the $\beta$ should be large to focusing more on current batch statistics. $\\beta$ estimated layer by layer.

- **Reduce C**: trivially pruning channels would cast serious issues, especially when some channels are critical for OOD generalization. 
  - This paper: unconditioned pruning strategy by repeatedly generating a stochastic mask M per iteration such that q*100% entries of the mask are zeros and the rest are ones. Given the input tensor z to the affine layer, we mask the tensor by z = Mz.
  - Pros: pruning lowers memory usage significantly with much smaller intermediate caches and gradients; mitigates catastrophic forgetting since only a subset of affine weights are updated and the low-magnitude parameters are not updated.

- **Dynamic L** (Train layers on demand): define a threshold $\beta_{\text{th}}$, if $\beta$ in reducing B is larger than this threshold, apply [Reduce C] above.

 <img width=700 alt="1685931298880" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6db9e7cf-1206-4bcb-867b-583ab7499c17">

### Experiments
- Dataset: CIFAR-10C/100C; ImageNet-C
- <img width=700 alt="1685931702092" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cb3effb9-8f00-43b9-84f0-1d535529501e">
- <img width=700 alt="1685931884551" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/0f91f3c9-4ee5-447a-892c-ce547e3881c3">

### Notes
