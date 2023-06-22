## [Test-Time Training with Masked Autoencoders](https://arxiv.org/pdf/2209.07522.pdf)

NeurIPS 2022

### Introduction and background
- For TTT tasks, still use the way that trains both the main task and the self-supervised task during training while only finetuning the self-supervised task during testing and then getting the test prediction from the main task.
- masked autoencoders (MAE): it splits each image into many (e.g., 196) patches, randomly masks out the majority of them (e.g., 75%), and trains a model to reconstruct the missing patches by optimizing the mean squared error between the original and reconstructed pixels.
- MAE pre-trains a large encoder and a small decoder, both ViTs. Only the encoder is used for a downstream task, e.g. object recognition. The encoder features become inputs to a task-speciﬁc linear projection head.
### Method
<img width=700 alt="aaa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/d59513c4-8e42-4f71-ad78-0fe562d38eac">

- This paper uses spatial autoencoding to remove parts of the data for the self-supervised task and then predict the removed content.
- Assume the feature extractor (MAE encoder) is $f$, the classifier is $h$, and the self-supervised head (MAE decoder) is $g$. During training time, we only update the classification head $h$ while keeping others frozen. Where $f_0$ and $g_0$ are pre trained MAE.
  By: <img width=280 alt="aaa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7bcbe8f9-f99d-4d0a-8ba1-389feadb2bcc">

- During testing: only update MAE. After that, use $h(f(x))$ as the test-time model prediction.

  <img width=280 alt="aaa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/707910cc-b858-4ca1-ae59-712a2230ee76">

### Experiments
- ImageNet-C/A/R; Portraits
- Batch size: 128
- Steps: 20/10
 
### Notes
