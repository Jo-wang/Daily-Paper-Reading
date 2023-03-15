## [Dataset Distillation by Matching Training Trajectories](https://openaccess.thecvf.com/content/CVPR2022W/VDU/papers/Cazenavette_Dataset_Distillation_by_Matching_Training_Trajectories_CVPRW_2022_paper.pdf)

CVPR 2022

### Introduction and background
- Definition: Dataset distillation is the task of synthesizing a small dataset such that a model trained on the synthetic set will match the test accuracy of the model trained on the full dataset.
- 
<img width=300 alt="1678878542669" src="https://user-images.githubusercontent.com/46414159/225291784-0ff1236f-c2b3-4b80-9ee6-d222c204eeef.png">

- end-to-end training requires huge compute and memory and suffer from inexact relaxation or training instability of unrolling many iterations.
-  short-range behavior, enforcing a single training step on distilled data to match that on real data. However, error may accumulate in evaluation.
- This paper: matching segments of parameter trajectories trained on synthetic data with segments of pre-recorded trajectories from models trained on real data. By treating the real dataset as the gold standard for guiding the network’s training dynamics, the synthetic dataset can be distilled to induce a network's training dynamics to follow the expert trajectory. If successful, this approach would allow the synthetically trained network to achieve similar test performance to the model trained on real data, by landing at a place close to the real model in the parameter space.

### Method

- **Question one**: How to obtain expert trajectories?

  Define it: The expert trajectories is defined as the time sequence of parameters obtained during the training of a neural network on the full, real dataset.

  How to save it:  train a large number of networks on the real dataset and save their snapshot parameters at every epoch. denoted as $\theta ^*$

  The corresponding student parameter: $\hat{\theta}$

  Goal: Our goal is to distill a dataset that will induce a similar trajectory (given the same starting point) as that induced by the real training set such that we end up with a similar model. 
  
- **Question two**: How to match the expert parameter with their corresponding student one?

<img width=300 alt="1678882761048" src="https://user-images.githubusercontent.com/46414159/225307005-81c446a7-b2c3-452a-8c4d-7ad3687a6729.png">

  Step 1: sample parameters from one of our expert trajectories at a random timestep t and use these to initialize our student parameters $\hat{\theta}_t := \theta ^* _t$
  
  Step 2:  perform N gradient descent updates on the student parameters with respect to the classification loss of the synthetic data (with differentiable augmentation and trainable learning rate, i.e. lr = nn.Parameter(torch.Tensor([0.01]), requires_grad=True) ) p.s. we do use the same types of differentiable augmentations on real data during the generation of the expert trajectories.
  
  Step 3: update our distilled images according to the weight matching loss: i.e., the normalized squared L2 error between the updated student parameters at t+N and the known future expert parameters at t+M
  
  Step 4:  minimize objective to update the pixels of our distilled dataset, along with trainable learning rate, by back-propagating through all N updates to the student network. 
  
- **Question three**: how to satisfy the memory limitation?

  Previous method: distill one class at a time
  
  Our method: sample a new mini-batch at every distillation step (but may have reduntant info)
  
  So, sample a new mini-batch b for every update of the student network(i.e.,the innerloop in Line 10 of Algorithm 1) such that all distilled images will have been seen by the time the final weight matching loss is calculated.
  
### Experiments
- dataset: 32*32 CIFAR-10 and 100; 64*64 Tiny ImageNet; 128*128 ImageNet subset

- evaluation: training a randomly initialized neural network from scratch on distilled data and evaluating on the validation set.

- baselines: Dataset Distillation(DD), Flexible Dataset Distillation(LD), Dataset Condensation(DC), and Differentiable Siamese Augmentation(DSA), along with a method based on the infnite-width kernel limit(KIP) and concurrent works Distribution Matching(DM) and Aligning Features(CAFE). instance selection algorithms including random selection (random), herding methods(herding), and example forgetting(gorgetting)

<img width=400 alt="1678883691221" src="https://user-images.githubusercontent.com/46414159/225310294-e2b3f69c-3698-4e5b-8f42-80e4c1ff989d.png">

### Notes
differentiable augmentation: The key idea behind differentiable augmentation is to make the augmentations differentiable with respect to the network parameters. This allows the network to learn how to effectively use the augmented data during training, and the gradient information can be backpropagated through the augmentations to update the network weights. In this way, differentiable augmentation can help the synthetic dataset to better capture the variability of the real-world data, leading to improved accuracy when training on the synthetic data.
