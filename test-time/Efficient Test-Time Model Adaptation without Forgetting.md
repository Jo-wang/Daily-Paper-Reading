## [Efficient Test-Time Model Adaptation without Forgetting](https://arxiv.org/abs/2204.02610)
ICML2022

Ranking: 

### Introduction and background
- existing methods have to perform backward computation for each test sample, resulting in unbearable prediction cost to many applications
- Other TTA solution suffer from severe performance degradation on in-distribution data after TTA (known as catastrophic forgetting)
- xxx

### Method

![Screen Shot 2022-12-20 at 15 31 20](https://user-images.githubusercontent.com/46414159/208591111-ff452dee-6968-438b-bfa5-6e76d8b2b77d.png)

- **Formulation:**
  - Distrbution of training data $P(x)$;
  - base model trained on training data $f_{\theta^{o}}(x)$
  - OOD test distribution $Q(x)$, where $P(x)\neq Q(x)$ 
  - Note that the test data could be either ID or OOD
 
![Screen Shot 2022-12-20 at 16 32 30](https://user-images.githubusercontent.com/46414159/208599266-cb1d9dd7-e776-4d83-ab59-c1fbfe7c93b1.png)


- **Sample Efficient Entropy Minimization**: efﬁcient adaptation relying on an active sample selection strategy
$S(x)$ is active sample selection score measure if one sample is reliable and not redundant. (if $S(x)=0$, skip this data)
The sample-efficient entropy minimization:
![Screen Shot 2022-12-20 at 16 36 01](https://user-images.githubusercontent.com/46414159/208599749-a420d9f9-6641-44b4-8b0f-ff57a2547604.png)
  - Reliable Sample Identification: low-entropy sample more contribute to the learning; high entropy on test sample will hurt the performance (uncertain)
![Screen Shot 2022-12-20 at 16 41 19](https://user-images.githubusercontent.com/46414159/208600481-4b07d5cc-2afa-4d65-88eb-d22925db5b7c.png)
This exclude partial unreliable samples, but the remaining samples may have redundancy.
- Non-redundant Sample Identification: Use EMA to track average model outputs of all seen test samples
![Screen Shot 2022-12-20 at 16 58 50](https://user-images.githubusercontent.com/46414159/208603170-e39f4ffa-679e-4a04-b2f2-6b86a1b11aa3.png)
**All in all, do not backward of a sample is high entropy or redundant.**

- Anti-forgetting with Fisher Regularization
   - Use a importance-aware regularizer $R$ yp prevent the model para from changing too much:
   - ![Screen Shot 2022-12-20 at 17 20 24](https://user-images.githubusercontent.com/46414159/208606775-155a60eb-a71f-4761-8d8e-b5056b008f33.png)
$w(\theta_{i})$ is the importance of $\theta_{i}$ and measure it via the diagonal Fisher information matrix. 
Since there is no ID training data during test-time, we use ID test and their corresponding plabels as pseudo-labeled ID test set $D_{F}={ x_{q},\hat {y_{q}} }$

![Screen Shot 2022-12-20 at 17 25 36](https://user-images.githubusercontent.com/46414159/208607689-facb0e5d-fafe-4195-a77f-04efcd547e70.png)

The final optim is:
![Screen Shot 2022-12-20 at 17 26 18](https://user-images.githubusercontent.com/46414159/208607828-81c2cf93-6641-465b-a900-53a7969f9feb.png)


### Experiments

- dataset: CIFAR-10-C, ImageNet-C, ImageNet-R
- Model: ResNet-26, ResNet-50
- Evaluation: 
  - 1. Clean accuracy/error on origional ID test samples; 
  - 2. OOD accuracy/error on OOD test samples; 
  - 3. Num of forward and backward passes

![Screen Shot 2022-12-20 at 17 30 59](https://user-images.githubusercontent.com/46414159/208608745-54652715-5539-4b6d-90b7-46a17b39107f.png)
![Screen Shot 2022-12-20 at 17 31 16](https://user-images.githubusercontent.com/46414159/208608802-73f8e9af-7ce1-4f19-a3ef-8f32494fa35f.png)


### Notes
