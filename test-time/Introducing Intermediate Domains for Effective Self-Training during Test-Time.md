## [Introducing Intermediate Domains for Effective Self-Training during Test-Time](https://arxiv.org/abs/2208.07736)

NOT EVEN SOURCE-FREE! ONLY updating multiple times can surpass the baselines.

### Introduction and background
- First, adapting a model to long test sequences that contain multiple domains can lead to error accumulation.
- Second, naturally, not all shifts are gradual in practice.

### Method
<img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a23be18e-7928-4581-acde-2d017eddcdda">

#### Generating intermediate domains
- MixUp: Since test samples are label-free, we only interpolate source sample $x_j^S$ with the test sample $x_{t i}^T$ from the current test batch $x_t^T$ that has the highest similarity in terms of the largest dot product in the output softmax probability space.
  
  <img width=300 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2a6e2cd9-ed65-4ee8-a564-f0326f0a8fab">
  
- Style transfer:
  
 <img width=400 alt="a2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/db6587bc-5d8a-43bb-b20a-aa27c563c33e">

#### Self-training
Using a threshold that filters out all pseudo-labels below an adaptively defined (softmax) confidence level:

 <img width=400 alt="afef" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/068bdd66-6dc9-4af1-bd5d-a46eeb697dd8">

 where $p$ is softmax output.

 Then pseudo-label-based CE loss is to update the model.

### Experiments
- create new dataset: CarlaTTA absed on CARLA
- cifar10c, cifar100c, imagenetc
### Notes
