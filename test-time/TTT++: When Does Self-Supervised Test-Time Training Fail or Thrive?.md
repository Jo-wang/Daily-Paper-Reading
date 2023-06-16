## [TTT++: When Does Self-Supervised Test-Time Training Fail or Thrive?](https://proceedings.neurips.cc/paper_files/paper/2021/hash/b618c3210e934362ac261db280128c22-Abstract.html)

NeurIPS2021

### Method
#### Define TTT (test-time training)
- shared encoder $g$, main task head $\pi_m$ (pred classes) and self-supervised head $\pi_s$ (pred rotation, etc.)
- The aim of TTT is fine-tune the encoder $g$ based on the self-superivsed task with the test samples, with the hope that the updated model $\pi_m \circ g^\prime$ yields improved results on the main task.

#### Online feature alignment
- offline feature summarization: calculate the the first and the second moments of source (i.e., mean and variance)
- minimizing the distance between the feature statistics estimated **from a mini-batch of test samples** (i.e., $\mu_z^{\prime}$ and $\Sigma_z^{\prime}$) and the pre-stored quantities about the training domain: $\mathcal{L}_{f, z}=\left\||\mu_z-\mu_z^{\prime}\right\||_2^2+\left\||\Sigma_z-\Sigma_z^{\prime}\right\||_F^2$ where $\||\cdot\||_2$ is Euclidean norm and $\||\cdot\||_F$ is Frobenius norm.
- To solve the problem of low-order statistics may be insufficient to fully capture complex distributions in high dimensions, align the feature distributions at both the **output of the encoder and the output of the self-supervised head**.
- 
#### Online dynamic queue

#### TTT through contrastive learning

### Experiments
- dataset: Cifar10C/100C/10.1; VisDA-C
- ResNet-50
### Notes
