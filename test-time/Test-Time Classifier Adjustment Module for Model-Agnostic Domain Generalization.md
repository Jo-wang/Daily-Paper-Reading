## [Test-Time Classifier Adjustment Module for Model-Agnostic Domain Generalization](https://openreview.net/forum?id=e_yvNqkJKAW)

NeurIPS2021

### Introduction and background
- **Background:**
Deep neural networks have achieved remarkable success in various machine learning tasks, but they often suffer from poor generalization performance when the test data comes from a different distribution than the training data. This is known as the domain shift problem, and it can significantly affect the accuracy and reliability of machine learning models in real-world scenarios.

- **Motivations:**
The main motivation of this paper is to address the domain shift problem in deep neural networks by proposing a new method for model-agnostic domain generalization. 

  Specifically, the proposed Test-Time Classifier Adjustment Module for Model-Agnostic Domain Generalization (T3A) aims to make machine learning models more robust to unknown distribution shifts during test time by correcting predictions during test phase, rather than just training phase.

  The authors also aim to demonstrate that T3A is computationally efficient, applicable to different types of deep neural networks, and can be used together with existing DG algorithms.

  Overall, this paper seeks to improve the generalization performance of deep neural networks in real-world scenarios where the test data may come from a different distribution than the training data.

### Method T3A
<img width=550 alt="1684977500378" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9f0c5961-2172-489e-9e30-0b82de376acf">

1. Freeze feature extractor, for the classifier with parameter $\omiga$, treat it as prototype. For the sample similarity for each of the prototype:

<img width=300 alt="image" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8d6da5b4-5e9c-49f5-93ac-195ab76bf7dd">

2. Maintain K support set, for each sample x, according the prediction above, update the support set:

<img width=300 alt="1684981180085" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bed83a9c-a13d-4efc-9304-40a0e0d42bfa">

where <img width=100 alt="1684981313209" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/827f6b6e-3631-4eda-9498-4123a6534c1e">

3. Predict according to the new support set:

<img width=600 alt="1684981555613" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/e8cdb5cf-6933-458f-8170-8d2684921712">

<img width=600 alt="1684981664104" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9e949bb9-f62a-4030-813b-3d9b8d935d75">

- **Conclusion: T3A implicitly reduces prediction entropy; T3A is computationally light; Adjusting the linear classifier can significantly improve performance.

### Experiments

### Notes
