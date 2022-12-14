## [Assaying Out-Of-Distribution Generalization in Transfer Learning](https://arxiv.org/abs/2207.09239)
NeurIPS2022

Ranking: 4

### Introduction and background
- Main Focus： 
  - (1) What are good proxy measures of OOD robustness when having access to a single dataset? 
  - (2) How do architecture choices and fine-tuning strategies affect robustness? 
  - ![1670894165484](https://user-images.githubusercontent.com/46414159/207202246-dc38d551-8597-471c-ade6-3f78dfeccb52.png)


### Method
#### Factor analysis
![Screen Shot 2022-12-14 at 16 38 11](https://user-images.githubusercontent.com/46414159/207524187-e2e4c012-bada-43f4-b5b7-626d7c1f1e03.png)
![Screen Shot 2022-12-14 at 17 04 30](https://user-images.githubusercontent.com/46414159/207528439-de0a64c8-a5e1-4a7e-909b-8f3dcb8ca81d.png)
- Accuracy is the strongest ID predictor of OOD robustness and models that generalize well in distribution tend to also be more robust. Evaluating accuracy on additional held-out OOD data is an even stronger predictor.
- - Other metrics can add marginal additional information for OOD robustness. Calibration appears to be predictive of ID accuracy but does not transfer to new distributions and adversarial robustness appears not to reﬂect robustness to natural distribution shifts. Corruptions are only marginally useful for measuring robustness to natural distribution shifts and should not be used as a substitute to real held-out OOD data. ImageNet upstream performance provides information on downstream robustness. However, robustness to commonly used shifts of ImageNet does not imply downstream robustness more than the clean upstream accuracy.
![Screen Shot 2022-12-14 at 17 22 48](https://user-images.githubusercontent.com/46414159/207531466-33f7ccfa-a6d9-4bd7-9783-e727dc5d268a.png)
- Among all metrics adversarial robustness transfers best from ID to OOD data, which suggests that models respond similarly to adversarial attacks on ID and OOD data. Calibration transfers worst, which means that models that are well calibrated on ID data are not necessarily well calibrated on OOD data.
- The effect of augmentations, ﬁne-tuning strategy and few-shot learning
![Screen Shot 2022-12-14 at 17 23 44](https://user-images.githubusercontent.com/46414159/207531655-1035c5d7-983a-4691-8c46-6f7ae38986d1.png)
  - Augmentations can improve accuracy and robustness to all kinds of distribution shifts (artiﬁcial and adversarial corruptions, OOD generalization), especially when data is scarce. While ﬁne-tuning the full architecture is beneﬁcial when having access to the full dataset, ﬁne-tuning the head only can lead to higher robustness in the low data regime.
### Experiments
#### Setup
- Experimental protocol and datasets: publicly available pre-trained weights for ImageNet1k / ILSVRC2012; 36 datasets grouped into ten different tasks sharing the same labels. For each task, we take a single training dataset to fine-tune the model and report evaluation metrics on both its ID test set and all the other OOD test sets. We extract 172 (ID, OOD) dataset pairs from the different domains of the ten tasks: DomainNet, PACS, SVIRO, Terra Incognita as well as the Caltech101, VLCS, Sun09, VOC2007 and the Wilds datasets.
- Evaluation on ID, OOD and corrupted data: 17 types of corruptions
- Models: Resnet50d, DenseNet, EfficientNetV2, gMLP, MLP-Mixer, ResMLP, Vision Transformers1, Deit, Swin Transformer
- Model hyperparameters and augmentation strategies: 1.  learning rate and the number of fine-tuning epochs; 2. standard ImageNet augmentation, RandAugment, AugMix
- Fine-tuning strategy and few-shot training: fine-tuning the full architecture and fine-tuning only the head. 
  Three training paradigms: training on the full downstream dataset, and two few-shot settings: “few-shot-100” (a subset with 100 examples per class, if available) and “few-shot-10” (with 10 examples per class). 
- Metrics: classification error, negative log-likelihood (NLL), demographic disparity on inferred groups as a measure of invariance, the expected calibration error (ECE), and adversarial classification error for two different $L_{2}$-attack sizes.
### Notes
This is an empirical study of ID and OOD accuracy in terms of different factors.
