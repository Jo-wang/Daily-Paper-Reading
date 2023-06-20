## [Test-Time Prompt Tuning for Zero-Shot Generalization in Vision-Language Models](https://arxiv.org/pdf/2209.07511.pdf)

NeurIPS2022

### Introduction and background
- The motivation of this paper is to address the challenge of zero-shot generalization in vision-language models. 
- While pre-trained models have shown impressive performance on in-domain tasks, they often struggle to generalize to unseen domains and categories. 
- The authors aim to improve the generalization capability of vision-language models by introducing test-time prompt tuning (TPT). 
- TPT allows the model to dynamically adapt its prompts during inference, enabling it to handle unseen data better and achieve higher accuracy in zero-shot scenarios. 
- The motivation is to explore the potential of prompt tuning as a means to enhance the robustness and generalization of large-scale foundation models in machine learning systems.

### Method
<img width=600 alt="aa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/da54af86-520b-47c3-a5a6-48cabf069f5e">

#### CLIP
- CLIP has two parallelled encoders: $\mathcal{F}=\{E_{\text{visual}}, E_{\text{text}}\}$
- For a sample $X$, we have a hand-crafted prompt prefix $p=\text{"A photo of a "}$ to every $y_i$ in the label set $\mathcal{Y}$. We can get the text feature $t_i$ for each label $i$ by $t_i=E_\text{text}(p ; y_i)$
- We can get the image feature by $v=E_\text{visual}(X)$
- Compute the similarity score and get the prediction probability by: <img width="200" alt="ssf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ec8ef7b0-4b75-4b0e-b360-7c9b83755b6e">

### Experiments

### Notes
