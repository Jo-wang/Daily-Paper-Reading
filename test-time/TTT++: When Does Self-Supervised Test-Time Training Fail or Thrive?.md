## [TTT++: When Does Self-Supervised Test-Time Training Fail or Thrive?](https://proceedings.neurips.cc/paper_files/paper/2021/hash/b618c3210e934362ac261db280128c22-Abstract.html)

NeurIPS2021

### Method

<img width=600 alt="a1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a6614e38-d038-4ca5-8fca-1833c37f4028">


#### Define TTT (test-time training)
- shared encoder $g$, main task head $\pi_m$ (pred classes) and self-supervised head $\pi_s$ (pred rotation, etc.)
- The aim of TTT is fine-tune the encoder $g$ based on the self-superivsed task with the test samples, with the hope that the updated model $\pi_m \circ g^\prime$ yields improved results on the main task.

#### Online feature alignment
- offline feature summarization: calculate the the first and the second moments of source (i.e., mean and variance)
- minimizing the distance between the feature statistics estimated **from a mini-batch of test samples** (i.e., $\mu_z^{\prime}$ and $\Sigma_z^{\prime}$) and the pre-stored quantities about the training domain: $\mathcal{L}_{f, z}=\left\||\mu_z-\mu_z^{\prime}\right\||_2^2+\left\||\Sigma_z-\Sigma_z^{\prime}\right\||_F^2$ where $\||\cdot\||_2$ is Euclidean norm and $\||\cdot\||_F$ is Frobenius norm.
- To solve the problem of low-order statistics may be insufficient to fully capture complex distributions in high dimensions, align the feature distributions at both the **output of the encoder and the output of the self-supervised head**.
- The final objective at test time is a weighted combination of the self-supervised loss, the feature alignment loss at the encoder and that at the self supervised head: 
  $L_\text{TTT++}=L_{s} + \lambda_{z} L_{f, z}+\lambda_s L_{f, s}$

#### Online dynamic queue
Previously it said that use batch-level statistics to align the domain, here we could further construct a dynamic queue that contains a few batches of feature vectors encoded at test time. We progressively update the queue by appending the latest mini-batch and popping out the oldest one, to calculate the $\mu_z^{\prime}$ and $\Sigma_z^{\prime}$
#### TTT through contrastive learning
- augment each image in a mini-batch to two ivews, then treat two augmented views from the same original instance as a positive pair and treat the other pairs as negative ones
- The feature vector $z_i$ from encoder $g(x_i)$ will be inputed to self-supervised head $h_i = \pi_{s}(z_i)$
- positive pair < $h_i, h_j$ > are expected to be close and any others should be further. <img width=300 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/16865111-a9cf-4733-b33e-a5c2de11d9c3">
- sim($\cdot$) is cosine similarity.
### Experiments
- dataset: Cifar10C/100C/10.1; VisDA-C
- ResNet-50
### Notes
