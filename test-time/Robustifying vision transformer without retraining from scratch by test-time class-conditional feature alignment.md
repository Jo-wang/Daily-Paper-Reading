## [Robustifying vision transformer without retraining from scratch by test-time class-conditional feature alignment](https://arxiv.org/abs/2206.13951)

IJCAI2022


### Method
- Use transformer instead of resnet family as the backbone.
- Test to update layernorm/cls token/encoder/all parameter
- Use global/class level domain alignment by the $\mu$ and $\Sigma$
- Need to store the source class/global statistics.

### Experiments
- ViT-AugReg, DeiT, and BeiT, ResNet, MLP-Mixer
- (CIFAR-10-C, CIFAR-100-C, and ImageNet-C, digits datasets and ImageNet-Sketch

