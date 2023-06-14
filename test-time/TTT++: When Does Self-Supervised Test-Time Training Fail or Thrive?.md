## [TTT++: When Does Self-Supervised Test-Time Training Fail or Thrive?](https://proceedings.neurips.cc/paper_files/paper/2021/hash/b618c3210e934362ac261db280128c22-Abstract.html)

NeurIPS2021

### Method
#### Define TTT (test-time training)
- shared encoder $g$, main task head $\pi_m$ (pred classes) and self-supervised head $\pi_s$ (pred rotation, etc.)
- The aim of TTT is fine-tune the encoder $g$ based on the self-superivsed task with the test samples, with the hope that the updated model $\pi_m \circ g^\prime$ yields improved results on the main task.

#### Online feature alignment

#### Online dynamic queue

#### TTT through contrastive learning

### Experiments
- dataset: Cifar10C/100C/10.1; VisDA-C
- ResNet-50
### Notes
