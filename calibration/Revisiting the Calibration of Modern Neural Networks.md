## [Revisiting the Calibration of Modern Neural Networks](https://arxiv.org/abs/2106.07998)

NeurIPS 2021

Ranking: :star: :star: :star: :star:

### Introduction and background
- 1. The best current models, including the non-convolutional MLP-Mixer and Vision Transformers, are well calibrated compared to past models and their performance is more robust to distribution shift.
- 2. In-distribution calibration slightly deteriorates with increasing model size, but this is outweighed by a simultaneous improvement in accuracy.
- 3. Under distribution shift, calibration improves with model size, reversing the trend seen indistribution.
- 4. Accuracy and calibration are correlated under distribution shift, such that optimizing for accuracy may also benefit calibration.
- 5. Model size, pretraining duration, and pretraining dataset size cannot fully explain differences in calibration properties between model families.
- Measurement: ECE, likelihood, Brier score, Bayesian methods, conformal prediction
- Improving calibration: post-hoc rescaling of predictions, averaging multiple predictions, data augmentation 

### Method

### Experiments

### Notes
