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

### Experiments

### Notes
