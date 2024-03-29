
## [Neuro-Modulated Hebbian Learning for Fully Test-Time Adaptation](https://arxiv.org/pdf/2303.00914.pdf)

CVPR2023

### Introduction and background
- This paper divide the source-free UDA into two: 1. need to access the whole dataset; 2. fully test-time adaptation, only needs access to live streams of test samples. And this paper focuses on the second type.
- Main challenge is how to learn useful early layer representations of the test samples without supervision
- Hebbian learning: It describes how neurons can change their connections based on the correlation between their activities. In other words, it states that if two neurons fire together, the connection between them is strengthened, while if they don't fire together, the connection is weakened. The rule is often stated as "cells that fire together, wire together". 
- To apply Hebbian learning: The neuron responses are tuned based on a local synapse-change procedure and activated by competitive lateral inhibition rules. 
- the original hard decision for competitive learning is not suitable for fully test-time adaptation
- the Hebbian learning does not have an effective mechanism to consider external feedback, especially the feedback from the top network layers.

### Method
![1681871055199](https://user-images.githubusercontent.com/46414159/232950283-a5a59707-4b19-4065-9f90-096b8fee4cac.png)
- Hebbian rule: 
![1681960994252](https://user-images.githubusercontent.com/46414159/233250298-d9d8d39c-b939-455d-a2a1-d5bfb0872497.png)

### Experiments

### Notes
- free energy: In physics and statistical mechanics, free energy refers to the energy in a physical system that is available to do useful work. It is a thermodynamic quantity that combines the system's internal energy and its entropy, and it represents the maximum amount of work that can be obtained from a system at constant temperature and pressure. In the context of statistical physics and machine learning, free energy is also used as a measure of the quality of a probabilistic model or a generative model. In this case, free energy represents the difference between the true data distribution and the approximate distribution of the model, and minimizing free energy is a common objective in training these models.
