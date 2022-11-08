
## [Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks （MAML）](https://arxiv.org/abs/1703.03400)
ICML 2017

Ranking: 5

### Introduction and background
- 
- xxx
- xxx

### Preliminary
- Loss function $L(\phi)$ is a sum of all losses on different tasks; $l^{n}(\hat{\theta}^{n})$ is loss of task $n$ on the testing set of task $n$.
- $\hat{\theta}^{n}$ is model learned from task $n$, it depends on $\phi$ (init parameter).

### Method
- learn a initialization parameter by loss $L(\phi)$: Considering one-step training. $\hat{\theta} = \phi - \epsilon\Delta _{\phi}l(\phi)$
- Update parameter for multiple steps on meta test: 
- $\phi \gets \phi - \eta\Delta_{\phi}L(\phi)$
- $L(\phi)=$
### Experiments

### Notes
