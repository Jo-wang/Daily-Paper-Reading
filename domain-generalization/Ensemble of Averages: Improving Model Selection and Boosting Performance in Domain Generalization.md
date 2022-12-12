## [Ensemble of Averages: Improving Model Selection and Boosting Performance in Domain Generalization](https://arxiv.org/abs/2110.10832)
NeurIPS 2022

Ranking: 3

### Introduction and background
![1670803186510](https://user-images.githubusercontent.com/46414159/206936883-f5a47d8b-1a07-4eb0-8766-145b5cdec3db.png)

- model selection plays an important role in domain generalization
- the out-domain performance varies greatly along the optimization trajectory of a model during training, even though the in-domain performance does not. It hurts the reliability of model selection, and can become a problem in realistic settings where test domain data is unavailable
- **Model averaging -> Ensembling moving average model**
- This proposed model is: Hyperparameter-free; Computationally efficient; EoA is better than non-avg model

### Method
1. Model Averaging: Start from a certain iter rather than from the beginning, end at the end of training.![1670803932871](https://user-images.githubusercontent.com/46414159/206937485-f549b849-310c-4edc-9976-8509f3598455.png)
and ![1670803954862](https://user-images.githubusercontent.com/46414159/206937507-8b671397-8df9-4400-9186-b7a65c75c397.png)
where $\hat{\theta_{t}}$ is the online model. Then choose the best validation $\hat{\theta_{t_{*}}}$ as the model to predict test dataset.   
**Benefit:**  the rank correlation between in-domain validation accuracy and out-domain test accuracy is significantly better when predictions are made using $\theta_{t}$. Makes the model selection more reliable.
![1670804568600](https://user-images.githubusercontent.com/46414159/206938074-18710ac8-cf5b-4b15-9617-8cd0e028db13.png)

2. Ensemble of Averages (EoA)
![1670806620354](https://user-images.githubusercontent.com/46414159/206940136-b216a280-f14a-4cb4-837b-72717b5b1a67.png)
Ensemble of multiple independently trained models (i.e., with different hyper-parameters and seeds), and each of these models are **moving average models from their corresponding runs**.
![1670806510385](https://user-images.githubusercontent.com/46414159/206940008-156a19d6-d91b-4d16-b133-16e4a62666f8.png)

### Experiments

### Notes
