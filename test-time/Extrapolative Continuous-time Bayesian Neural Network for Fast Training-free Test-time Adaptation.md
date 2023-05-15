## [Extrapolative Continuous-time Bayesian Neural Network for Fast Training-free Test-time Adaptation](c)

NeurIPS 2022

OTTA
### Introduction and background
- Real-world non-stationary streaming data usually are highly uncertain in their temporal dynamics
- Only partial observation of the time series or the local streams is available, resulting in poor alignment quality.
- To solve the first problem, formulating internal predictive modeling as a continuous-time Bayesian filtering problem within a stochastic dynamical system context.
- To solve the second problem: perform UDA on the entire data generation mechanism, which is described by a latent stochastic process conditioned on historical data. particle filter differential equation (PFDE)

### Method
![1684149407425](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/0e969a13-72bb-469f-bd1b-2d8313cd5609)

#### Particle Filter Differential Equation (PFDE)
![1684150218646](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e2e9c8ac-0aaf-4211-80a5-63dda313cfe5)
where ()'' is second order temporal derivative.
### Experiments

### Notes
