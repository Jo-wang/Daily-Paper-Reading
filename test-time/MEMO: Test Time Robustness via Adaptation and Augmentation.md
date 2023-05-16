## [MEMO: Test Time Robustness via Adaptation and Augmentation](https://proceedings.neurips.cc/paper_files/paper/2022/hash/fc28053a08f59fccb48b11f2e31e81c7-Abstract-Conference.html)

NeurIPS2022

### Introduction and background
- methods require specialized training procedures, and they typically rely on extracting information via batches or entire sets of test inputs, thus introducing additional assumptions.
- Our method, "plug and play"; synergize with other robustification techniques
- propose marginal entropy minimization with one test point (MEMO)

### Method
![1684199636607](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/27171c9d-7fc3-49dd-854f-2707bf521ef3)

![1684200138601](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/3ebbfe4d-12e3-45a8-bd1d-a790e225390a)

- For each batch with batch size B, sample B augmentations in augmentation set and perform them to input data in order.
  - We want the prediction consistency for different augmentations
  - We want the model to be confident for its predictions
- min the Ent for the augmented data
- Modify the BN statistics: channelwise mean and variance estimated from this point are mixed with the the mean and variance computed during training according to a prior strength N:

<img width=250 alt="1684201204465" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/402a730c-92d9-4754-b436-b1aa3228818f">


### Experiments
![1684215571860](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1ff8dbfa-4ea5-41ca-977f-040ef2eafc1f)

### Notes
