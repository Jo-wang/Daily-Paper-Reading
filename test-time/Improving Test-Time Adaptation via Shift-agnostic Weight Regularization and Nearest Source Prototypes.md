## [Improving Test-Time Adaptation via Shift-agnostic Weight Regularization and Nearest Source Prototypes](https://arxiv.org/abs/2207.11707)

ECCV2022

### Introduction and background
- The motivation behind this paper is to propose a novel strategy that adjusts the pre-trained model using only unlabeled online data from the target domain, which enables the model to quickly adapt to a new environment without human intervention. 
- The proposed method includes two approaches: shift-agnostic weight regularization and nearest source prototypes, which aim to reduce distribution shift and improve performance. 
- The authors show that their method exhibits state-of-the-art performance on various standard benchmarks and even outperforms its supervised counterpart.

### Method

![1684312515521](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ad5299f1-ea95-4064-acc1-0c6c528eaa1e)

![1684312857326](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/97934ee9-937b-4496-ae70-bfabc722d924)

where e is encoder, c is classifier.

![1684312946872](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1d5cdd12-0f98-4be5-b105-56a21ddd235e)

1. Input the org img and aug img into source model and use cosine similarity to calculate the change of gradient. g is gradient vector. l is layer l, N is source sample.

![1684313759806](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6c671683-9cea-4751-8aab-a626c07c32c5)

v is min-max normalization in range [0,1].

![Screen Shot 2023-05-17 at 22 44 35](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b320f7f1-9201-4240-a827-d303329c3c6d)

2. The loss for test data adaptation is combioned with one ent minimization and one mean ent maximization.

- Summary: The **shift-agnostic weight regularization (SWR)** approach encourages updating the model parameters sensitive to distribution shift while slightly updating those insensitive to the shift, during test-time adaptation. This regularization enables the model to quickly adapt to the target domain without performance degradation by utilizing the benefit of a high learning rate. The authors propose a novel loss function that incorporates this regularization term, which can be easily integrated into any existing deep learning framework.

![1684312985893](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ab6b62d5-4a7d-4fae-b094-1fc0e366d441)

**Source prototype generation**
1. create a projector between encoder and classifier as H, get the latent embedding z of a sample from this projector. Use EMA to update the prototype q:
![Screen Shot 2023-05-17 at 23 03 26](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/24ae7614-e6ec-413c-9d8c-47f5338ee641)

2. Then we obtain transformation on the same sample x. Get the embedding z'. When optimizating, calculate the CE loss for both x and x's transformation prediction:

![Screen Shot 2023-05-17 at 23 08 10](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5c82b546-ae38-44c9-9c07-852b1e092ddf)

**Auxiliary task loss at test time**
After generating source prototype:

1. Use the same way to optimuize the main task (min ent and max mean ent)
2. Use CE(y(x), y(T(x))) to optimize the aux task.

![Screen Shot 2023-05-17 at 23 24 14](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e334f327-214c-4514-8499-00dc400d00a1)

- Summary: The **(non-parametric) nearest source prototypes (NSP)** approach is an auxiliary task that aligns the source and target features, which helps reduce distribution shift and leads to further performance improvement. The authors propose a nearest source prototype classifier that learns to classify unlabeled target data based on its similarity to labeled source data. This approach encourages the model to learn features that are invariant across domains and reduces the discrepancy between the source and target distributions.

### Experiments

### Notes
