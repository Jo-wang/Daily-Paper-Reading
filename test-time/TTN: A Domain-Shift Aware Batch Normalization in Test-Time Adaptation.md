## [TTN: A Domain-Shift Aware Batch Normalization in Test-Time Adaptation](https://arxiv.org/abs/2302.05155)

ICLR2023 Poster

### Introduction and background
- re-estimating normalization statistics using test data depends on impractical assumptions that a test batch should be large enough and be drawn from i.i.d. stream, and performance drop without the assumptions
- CBN (conventional batch norm) and TBN (transductive batch norm) are in a trade-off relationship
- Original TTN:
![1683948243999](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b9b173b3-3b68-45fb-b02a-8c552a3b4fdb)

### Method
![1683945668241](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e1f07e1f-7b92-4118-8790-3cff098f8aea)

The main focus is the post-training process:

![1683947792637](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bf945590-59ac-43b2-85cf-fc0c79bfbb4f)

- First compute thee gradient similarity for the transformation parameter $\eta$ and $\beta$ for source org image and augmented image, then transfer these similarity to distance. As below shows:

![1683947887304](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e43cdac5-dda8-4ab9-9641-00cd674bff6d)

After that, treat the set of distances of each layer as a prior A and uses these info to optimize $\alpha$

### Experiments

### Notes
