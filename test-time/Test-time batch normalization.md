## [Test-time batch normalization](https://arxiv.org/abs/2205.10210)

### Method
- The backpropogated loss on $y_i$ at BN layer is finally: $\frac{\partial \mathcal{L}}{\partial x_i}=\frac{\partial \mathcal{L}}{\partial y_i} \frac{\gamma}{\sigma_r}$
where $\gamma$ is the affine parameter and $\sigma _r$ is the running average variance.

- This paper propose gradient presevering batch normalization (GpreBN) : $y_i=\frac{\frac{x_i-\mu_c}{\sigma_c} \bar{\sigma}_c+\bar{\mu}_c-\mu}{\sigma} \gamma+\beta$, (originally: $y_i=\frac{x_i-\mu}{\sigma} \gamma+\beta$) where $\mu_c$ and $\sigma_c$ are the statistics for current batch, $\bar{\mu}_c$ and $\bar{\sigma}_c$ is the stop gradient backpropogation. $\mu$ and $\sigma$ are arbitrary non-learnable parameters to normalize the feature. 
- The backpropogation of GpreBN is: $\frac{\partial \mathcal{L}}{\partial x_i}=\frac{\partial \mathcal{L}}{\partial y_i} \frac{\partial}{\partial x_i}\left(\frac{x_i-\mu_c}{\sigma_c}\right) \frac{\bar{\sigma}_c}{\sigma} \gamma$ (originally is: $\frac{\partial \mathcal{L}}{\partial x_i}=\frac{\partial \mathcal{L}}{\partial y_i} \frac{\partial}{\partial x_i}\left(\frac{x_i-\mu}{\sigma}\right) \gamma$)
- This decoupled the backpropogation form (via $\mu_c$ and $\sigma_c$) and the selection of normalization statistics (via $\mu$ and $\sigma$)
- To stabilize the adaptation process, we perfer $\mu$ and $\sigma$ to be dataset-level. $\mu_r^t=\lambda \mu_c+(1-\lambda) \mu_r^t ;\left(\sigma_r^t\right)^2=\lambda \sigma_c^2+(1-\lambda)\left(\sigma_r^t\right)^2$
  where $\mu_r^t$ are current running mean. $\mu_c$ is batch level mean, $\lambda$ is . 
- Then mix the currrent running mean with source mean $\mu_r$: $\mu=\theta \mu_r^t+(1-\theta) \mu_r ; \sigma^2=\theta\left(\sigma_r^t\right)^2+(1-\theta) \sigma_r^2$
### Experiments

### Notes
