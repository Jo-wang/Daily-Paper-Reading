
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
- $L(\phi)=\Sigma_{n=1}^{N}l^{n}(\hat{\theta}^{n})$
- 为了防止二次微分，用
- $\frac{\partial l(\hat{\theta})}{\partial \phi_{i}} 	\approx \frac{\partial l(\hat{\theta})}{\partial \hat{\theta}_{i}}$
- $\nabla_{\phi} L(\phi)=\nabla_{\phi} \Sigma_{n=1}^{N} l^{n}\left(\hat{\theta}^{n}\right) = \Sigma_{n=1}^{N} \nabla_{\phi} l^{n}\left(\hat{\theta}^{n}\right) \approx \Sigma_{n=1}^{N} \nabla_{\hat{\theta} ^{n}} l^{n}\left(\hat{\theta}^{n}\right)$
### Experiments

### Notes
