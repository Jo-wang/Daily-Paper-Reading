
## [Test-Time Adaptation via Self-Training with Nearest Neighbor Information](https://openreview.net/forum?id=EzLtB4M1SbM)

ICLR2023 poster

Ranking: :star: :star: :star: :star:

### Introduction and background
- Current TTA fall into 3 categories:
  - norm-based: replaces the batch normalization (BN) statistics of the trained
model with the BN statistics estimated on test data (only update BN parameters)
  - Entropy minimization: fine-tune the trained feature extractor, which is the trained classifier except the last linear layer, by minimizing the prediction entropy of test data;
  - prototype-based: modifies a trained linear classifier (the last layer) by using the pseudo-prototype representations of each class and the prototype-based classification for test data, where the prototypes are constructed by previous test data and the prediction for the data from trained classifier

### Method
<img width="700" alt="image2" src="https://user-images.githubusercontent.com/46414159/218350617-28103a20-7149-4347-8aab-e605eb5eba20.png">

- feature extractor: $f_\theta$; classifier: $g_w$
- **1. Prototype-based classification in test-time adaptation**: support set $S_t$ is a set of test samples until time t. The support set is initialized with the weight of the last linear classifier
  <img width="700" alt="image1" src="https://user-images.githubusercontent.com/46414159/218349724-ae01b230-ed0b-4926-96f2-8559752ee10a.png">
  
  the prototype is the mean of the latent representation of all sample belongs to class k in support set, and we can use Eud distance or cosine similarity to compute the distance. The support examples with unconfident pseudo labels are regarded as unreliable examples and filtered out

  Update support set:
  <img width="700" alt="image3" src="https://user-images.githubusercontent.com/46414159/218353106-df25497b-09cf-4074-bc0c-edbdc20cee8d.png">

- **2. retrieve nearest neighbors**:
  <img width="700" alt="image4" src="https://user-images.githubusercontent.com/46414159/218353949-e8c48f8f-d4a2-44fd-8e62-8902e07ac71b.png">

- **3. obtain nearest-neighbor-based pseudo label**: calculate prototype $\mu$ by mean of adaptive module from all the same support set.

  <img width="700" alt="image5" src="https://user-images.githubusercontent.com/46414159/218356345-36df2daf-b080-4467-a160-268a8ab59aa8.png">

- 4. 
  <img width="700" alt="image6" src="https://user-images.githubusercontent.com/46414159/218358051-3f5bedbb-b69a-4bc5-9f5e-0684ed396457.png">

<img width="700" alt="image8" src="https://user-images.githubusercontent.com/46414159/218358483-7853a0fb-88f9-4c67-a70b-40745691a2bb.png">

- 5. Variant: TAST-BN, that fine-tunes the BN layers instead of adaptation modules. The support set stores the test data itself instead of the feature representations since the embedding space of the feature extractor steadily changes during the test time. 
  <img width="700" alt="image7" src="https://user-images.githubusercontent.com/46414159/218358366-12966135-d593-46ec-a0aa-fcf497145b07.png">




### Experiments

### Notes
