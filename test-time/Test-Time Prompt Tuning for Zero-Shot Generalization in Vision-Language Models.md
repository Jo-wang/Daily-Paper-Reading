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

#### Prompt tuning on Downstream data
- optimize the prompt $p$ in the text embedding space
- <img width=300 alt="as" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/a17a7386-0b46-4b34-86aa-89b188455103">

#### Context-dependent visual reasoning
- a test sample contains two sets of support images and a query image for evaluation
- The two sets of support images exemplify the presence and the absence of a human-object interaction (HOI) concept
- The model is then asked to infer whether the query image contains the underlying concept
- Each test sample $X$ captures a concept by presenting c = <s; a; o> (e.g., subject: human, action: ride, object: bike) in one set of support images (positive examples), while having the other set (negative examples) demonstrate c' = <s; a'; o>, where a' != a. $o$ and $a$ are not explicitly given but predicted by the model reasoning ability.
- This is training the model on a collection of similar tasks (using the Bongard-HOI training split) to make similar inferences on test samples at test time.
- When applying CLIP to this task, we do not use additional training data because CLIP has learned abundant visual concepts and thus is a natural fit for such visual reasoning tasks.

#### TPT: Test-Time Prompt Tuning

### Experiments

### Notes
