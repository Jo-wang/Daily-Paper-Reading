## [Decorate the Newcomers: Visual Domain Prompt for Continual Test Time Adaptation](https://arxiv.org/abs/2212.04145)

AAAI2023

### Introduction and background
- The background and motivation of this method is to address the problem of **Continual Test-Time Adaptation (CTTA)** in real-world applications. (deal with continual domain change) 

- Pre-trained models often suffer from performance degradation when applied to new and evolving environments, which can lead to catastrophic forgetting. 

- The authors propose a lightweight prompt approach that uses visual domain prompts to dynamically update a small portion of the input image pixels, achieving domain adaptation while mitigating the error accumulation problem. 

- The approach is designed to handle the problem from the input image level and avoid catastrophic forgetting by limiting domain-sensitive parameters from over-adaptation. 

- The proposed approach outperforms most state-of-the-art methods according to experiments on extensive benchmark datasets, covering both synthetic and real-world domain gaps.

### Method
<img width=700 alt="1685492997711" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/25616c49-27ef-456c-af08-e99b7f2a258b">

#### Continual test time adaptation via domain prompt

#### Homeostasis-based prompt adapting strategy

### Experiments

### Notes
