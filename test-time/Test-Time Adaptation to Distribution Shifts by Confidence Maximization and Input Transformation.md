## [Test-Time Adaptation to Distribution Shifts by Confidence Maximization and Input Transformation](https://openreview.net/forum?id=GOfGGASIUkg)

Rejected

### Introduction and background
- **Background:**

  Deep neural networks often exhibit poor performance on data that is unlikely under the train-time data distribution, for instance data affected by corruptions.

- **Motivation:**

  The motivation of this paper is to address the problem of poor performance of deep neural networks on shifted distributions. 
  
  The authors propose a method for test-time adaptation that can improve network performance on such shifted distributions by maximizing confidence and partially undoing the distribution shift through input transformation. 
  
  They introduce a novel loss function that replaces entropy with a non-saturating surrogate and adds a diversity regularizer based on batch-wise entropy maximization to prevent convergence to trivial collapsed solutions. 
  
  The proposed method is shown to significantly improve the performance of different pretrained models on challenging benchmarks like ImageNet-C and ImageNet-R.

### Method
#### Architecture
- This paper define to adapt the target data by target model g as $g=f \circ d$; where f is source model and d is additional trainable network.

  <img width=600 alt="1685062831281" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/31486797-4dc2-449a-b6e1-1f19aaf92d8e">

- The network $r$ contains conv3*3 + Group Norm + ReLU. So that the modulation parapeters of $g$ are $\phi=\left(\beta, \gamma, \tau, \psi, \theta^{\prime}\right)$, where $\theta^{\prime} \subseteq \theta$ is the subset of parameter on source model $f(\theta)$. 

- Adapting only the affine parameters of normalization layers in f while keeping parameters of convolutional kernels unchanged. Additionally, batch normalization statistics (if any) are adapted to the target distribution.

#### Adaptation Objective
- **$L_{\text{div}}$**: encourages predictions of the network over the adaptation dataset X
that match a target distribution

  <img width=600 alt="1685064318356" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/be4a57e4-7cbd-449a-9e48-dd2273a75f8c">
  
  Minimize the KL between true target distribution and the estimated target distribution with per-batch.
- **$L_{\text{conf}}$**: encourages high confidence prediction on individual datapoints
  <img width=600 alt="1685065947686" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6a3a355e-5891-42bd-8d80-432702858567">
  
  where: 
  
   <img width=600 alt="1685065970863" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/919c64c9-05fb-4b32-bb56-e46966fc2ba1">
  
  where o are the network’s logits

  <img width=600 alt="1685066077815" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/db160a9c-8188-47bc-9f36-bfa9a1be5b1c">

### Experiments
<img width=600 alt="1685066343208" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/22903d85-5800-4cd6-a62f-504bd03e0019">

<img width=600 alt="1685066434614" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/86a19674-6bff-40d0-b708-886e3125d2d3">

### Notes
