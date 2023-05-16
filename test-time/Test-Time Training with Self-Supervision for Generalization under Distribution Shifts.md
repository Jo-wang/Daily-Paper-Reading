## [Test-Time Training with Self-Supervision for Generalization under Distribution Shifts](https://arxiv.org/abs/1909.13231)

ICML2020

Could be OTTA 

### Introduction and background
- 1. Traditional machine learning assumes that training and test data come from the same distribution, which may not be true in practice.
- 2. Distribution shifts can occur due to changes in the environment, sensor noise, or other factors.
- 3. Existing methods for addressing distribution shifts include domain adaptation and meta-learning, but these methods have limitations.
- 4. Test-Time Training (TTT) is a novel approach that leverages self-supervised learning to adapt to distribution shifts at test time.
- 5. TTT has several advantages over existing methods, including simplicity, flexibility, and effectiveness on diverse image classification benchmarks.

### Method
1. Train a model on labeled data from the source domain using supervised learning.

2. At test time, obtain an unlabeled sample from the target domain.

3. Use the unlabeled sample to create a self-supervised learning problem, such as predicting rotations or colorization. This is done by applying a random transformation to the image (e.g., rotating it by a random angle) and then asking the model to predict the transformation that was applied.

4. Update the model parameters using backpropagation on this self-supervised task. This involves computing gradients with respect to both the supervised loss on the source domain and the self-supervised loss on the target domain.

5. Make a prediction on the original task (e.g., image classification) using the updated model parameters.

6. Repeat steps 2-5 for each test sample, allowing for online adaptation to distribution shifts.

The intuition behind TTT is that by creating a self-supervised learning problem at test time, we can use information from the target domain to update our model in a way that improves its performance on that domain. This allows us to adapt to distribution shifts without requiring labeled data from the target domain.

TTT has several advantages over existing methods for addressing distribution shifts, including simplicity, flexibility, and effectiveness on diverse image classification benchmarks aimed at evaluating robustness to distribution shifts. However, it also has limitations, including sensitivity to hyperparameters and potential overfitting to specific self-supervised tasks.

**Note that the main exp replace the BN with GN.**

### Experiments
The paper used ResNets as the backbone architecture for all experiments, with different numbers of layers depending on the dataset. For CIFAR-10, a 26-layer ResNet was used, while for ImageNet, an 18-layer ResNet was used.

Also have exp on VID-Robust and CIFAR-10.1.

![Screen Shot 2023-05-17 at 00 20 54](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/977617d9-dd4a-4dfa-97a6-d5d9b5b1c567)

![Screen Shot 2023-05-17 at 00 31 51](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/4439536c-6c52-4397-83b4-cface6386abd)

