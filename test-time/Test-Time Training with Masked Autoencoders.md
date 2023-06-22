## [Test-Time Training with Masked Autoencoders](https://arxiv.org/pdf/2209.07522.pdf)

NeurIPS 2022

### Introduction and background
- For TTT tasks, still use the way that trains both the main task and the self-supervised task during training while only finetuning the self-supervised task during testing and then getting the test prediction from the main task.
- masked autoencoders (MAE): it splits each image into many (e.g., 196) patches, randomly masks out the majority of them (e.g., 75%), and trains a model to reconstruct the missing patches by optimizing the mean squared error between the original and reconstructed pixels.
- MAE pre-trains a large encoder and a small decoder, both ViTs. Only the encoder is used for a downstream task, e.g. object recognition. The encoder features become inputs to a task-speciﬁc linear projection head.
### Method
- This paper uses spatial autoencoding to remove parts of the data for the self-supervised task and then predict the removed content.
- 
### Experiments

### Notes
