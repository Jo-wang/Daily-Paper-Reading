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

![image](https://user-images.githubusercontent.com/46414159/218645142-c5743197-a5c5-4abd-8bc7-d7421d246954.png)

### Method
- In distribution:     
![image](https://user-images.githubusercontent.com/46414159/218645359-224c06ef-bd4a-4aa5-bd26-df36bca890cd.png)

![image](https://user-images.githubusercontent.com/46414159/218645446-7da7619b-20f8-42fe-a84a-4c30681af731.png)

- Distribution shift:
![image](https://user-images.githubusercontent.com/46414159/218645573-1710a746-d39a-465d-8f1d-ab041fa203f7.png)
![image](https://user-images.githubusercontent.com/46414159/218645673-df9d2628-5c0b-41c6-929e-8aa8a47a2ff3.png)
![image](https://user-images.githubusercontent.com/46414159/218645853-6f6ff446-a0d2-46f9-90ed-7e59ad100b0f.png)

- different measurement:
![image](https://user-images.githubusercontent.com/46414159/218646035-d723a87a-ad43-41e4-9a5e-cc5941a040ef.png)

### Experiments

### Notes
