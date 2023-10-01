## [Towards Open-Set Test-Time Adaptation Utilizing the Wisdom of Crowds in Entropy Minimization](https://arxiv.org/pdf/2308.06879.pdf)
ICCV2023

### Introduction and background
- Min ent not good, even with static thresholding

### Method
- Compare the difference (of softmax output) between original source pre-trained model and the adapted model
- <img width=300 alt="aa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/358d8a2d-b1cd-45fe-a255-d1f87971b299">
- $\hat{y}$ is the adapted model ourtput and y~ is the source pretrained model output. If the confidence increased, learn it by min ent.
- Otherwise,<img width=200 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/36cace78-2c80-464d-bc8c-6898d3ee6c91">
- mean ent maximization.

- The only difference between this paper and "Improving test-time adaptation via shift-agnostic weight regularization and nearest source prototypes" is the indicator.


### Experiments
![image](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/037bed03-bae8-4556-8222-e8ce9465a1c8)

### Notes
