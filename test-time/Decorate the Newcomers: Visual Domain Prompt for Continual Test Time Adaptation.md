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
- Two prompt: **domain-specific (DSP) $\psi_\delta$; domain-agnostic (DAP) $\omega_\phi$** added upon a portion of the input image and the decorated image is then input into the source model for predictions.
- The input images $x^T$ is added by these two prompt by summing up point by point:  $x_p^T=x^T+\omega_\phi+\psi_\delta$
- **Prompt updating:** Student-teacher model. Uuse student to update teacher through EMA while keep source model frozen. (DSP: CE loss; DAP: regularization term to constrain those domain-sensitive parameters to alleviate the instability when facing domain changes)

#### Homeostasis-based prompt adapting strategy
- **DAP regularization: How to limit the parameter sensitive to domain change?** 
- Use Homeostatic Factor: <img width=300 alt="1685498370922" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9b96c4e9-82cc-4712-8355-20b4175139ff">
  
  where $\theta ^*$ is the parameter for the last minibatch of the previous domain. $\theta$ is the parameter that needs to be inferred, $\Lambda_i^\tau$ is the weight learnt by: <img width=200 alt="1685504852654" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9feb0fef-f85b-4e22-9e43-03387bd0aadd"> and need to be updated **for every new domain**.
  
  <img width=300 alt="1685505011106" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2db3c5f2-9675-4cd9-9011-d31065521017">
  
  and $\delta_i^\nu=\theta_{i(t)}^\nu-\theta_{i(t-1)}^\nu$

  v is the domain.

- To determine when need to update the wieght (when the target domain changed to another), uses confidence, if the confidence changed larger than the defined threshold S 

  <img width=200 alt="1685506355768" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/92e88836-8627-4a6e-be69-06c5cda0b779">

  see the data as from new domain.
  
- Objective:

  <img width=300 alt="1685506559852" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3165c830-7b6e-4340-b3ce-7219d1c6d00d">
  
  where f' is teacher network and f is student network.


### Experiments

### Notes
