## [Improving Test-Time Adaptation via Shift-agnostic Weight Regularization and Nearest Source Prototypes](https://arxiv.org/abs/2207.11707)

ECCV2022

### Introduction and background
- The motivation behind this paper is to propose a novel strategy that adjusts the pre-trained model using only unlabeled online data from the target domain, which enables the model to quickly adapt to a new environment without human intervention. 
- The proposed method includes two approaches: shift-agnostic weight regularization and nearest source prototypes, which aim to reduce distribution shift and improve performance. 
- The authors show that their method exhibits state-of-the-art performance on various standard benchmarks and even outperforms its supervised counterpart.

### Method

- The **shift-agnostic weight regularization** approach encourages updating the model parameters sensitive to distribution shift while slightly updating those insensitive to the shift, during test-time adaptation. This regularization enables the model to quickly adapt to the target domain without performance degradation by utilizing the benefit of a high learning rate. The authors propose a novel loss function that incorporates this regularization term, which can be easily integrated into any existing deep learning framework.

- The **nearest source prototypes** approach is an auxiliary task that aligns the source and target features, which helps reduce distribution shift and leads to further performance improvement. The authors propose a nearest source prototype classifier that learns to classify unlabeled target data based on its similarity to labeled source data. This approach encourages the model to learn features that are invariant across domains and reduces the discrepancy between the source and target distributions.

### Experiments

### Notes
