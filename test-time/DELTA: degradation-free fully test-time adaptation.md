## [DELTA: degradation-free fully test-time adaptation](https://arxiv.org/abs/2301.13018#:~:text=Fully%20test%2Dtime%20adaptation%20aims,differs%20from%20the%20training%20distribution)

ICLR2023 Poster

### Introduction and background
- test-time BN are completely affected by the currently received test samples, resulting in inaccurate estimates.
- parameter update is biased towards some dominant classes
- the defects can be exacerbated in more complicated test environments, such as (time) dependent or class-imbalanced data
- previous approaches work well in certain scenarios while show performance degradation in others due to their faults


### Method
- **Diagnosis I**: Normalization statistics are inaccurate within each test mini-batch.
- **Treatment I**: Test-time batch renormalization (TBR) is a simple and powerful tool to improve the normalization.
  - From: <img width=200 alt="image" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/76cecfaa-18c3-4df6-a662-a94e0c859706">

  - To: <img width=450 alt="image1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/617d8afb-e24e-4e6c-93e9-5f8ef3ca2fc3">

    <img width=450 alt="image2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/61cef070-d2f1-4546-b1ee-a6b9ac63f42b">

    where $v$ is the input feature and $v^*$ is the output feature.
    
  <img width=700 alt="image4" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/b0812a0e-d6a7-42bf-8ff8-fe49540fdc85">

- **Diagnosis II**: the test-time optimization is biased towards dominant classes.
  - Predictions are imbalanced, even for a model trained on class-balanced training data and tested on a class-balanced test set with Ptest(x; y) = Ptrain(x; y)
  - Predictions becomes more imbalanced when Ptest(x; y) != Ptrain(x; y)
- **Treatment II**: Dynamic online re-weighting (DOT) can alleviate the biased optimization.
  - use a momentum-updated class-frequency vector z, (init z by $z[k]=\frac{1}{K}, k=1,2, \cdots, K$)
  <img width=700 alt="image3" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/20d06f10-2b34-4edd-8cf8-5aa403bbc66a">
  
  Note: TBR will applied to line 3 of algorithm on forward pass.
  
### Experiments

### Notes
