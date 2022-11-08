
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
- ![Screen Shot 2022-11-08 at 22 08 48](https://user-images.githubusercontent.com/46414159/200563385-11b18d03-b2a8-48ce-b987-81c0e04e5223.png)
- $\phi _{0}$ 是模型初始参数，用它和task $m$ 的support set计算m的模型参数 $\hat{\theta}^{m}$
- 用m的模型 $\hat{\theta}^{m}$ 带入 $m$ 的query set，来更新 $\phi _{0}$ 到 $\phi _{1}$
### Experiments

### Notes
