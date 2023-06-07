## [Multi-step test-time adaptation with entropy minimization and pseudo-labeling](https://www.notion.so/Multi-step-test-time-adaptation-with-entropy-minimization-and-pseudo-labeling-2dd145c1ed6444af841a46278bec2f1b?pvs=4)

ICIP2022

### Method
<img width=350 alt="img" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/008be8dd-7a33-4a99-bafd-5fbe9aea80a1">

<img width=350 alt="img1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6ef339cd-da1c-44b1-b8aa-cb26531dc196">

- **Not sure if this paper can fall into the online TTA category since it does backpropogation twice for each mini-batch.**
- First backpropogation: Update BN parameter by:

  <img width=350 alt="img2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5b8bfb0e-5ba4-4560-a1d5-9129a8da8be9">

- Then, update the FC layer by pseudo label with label smoothing

### Experiments
- CIFAR10C/100C
- ResNet-20; ResNet-56; WRN-28-10

<img width=600 alt="img3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/83c9e5f4-fb7b-4008-a172-70b57bbf215d">
