## [Online Adaptation to Label Distribution Shift](https://arxiv.org/abs/2107.04520)

NeurIPS2021

### Introduction and background
- This paper focusing on OTTA with label shift. Test-time label distribution is continually changing.
- Define the problem: online label shift, which is more common compared with offline case.
- Under this setting, the true label of test data and any incurred loss are both unobserved.
- The learner does not receive any feedback after making a prediction. (different from online learning)

### Method
- Online Gradient Descent
- Follow The History: (Similar idea as Follow The Leader (FTL) the predictor for time step is the one that minimizes the average loss from the previous time steps.) 
This paper uses Follow The Fixed Window History (FTFWH).
![1683697990699](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/73693c5b-f9b5-4c9e-83c0-0fb2d43a7177)

### Experiments
![1683698557004](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/0cd9b5fa-e8ab-4a23-8dcd-4b89c37d9e0b)
![1683698596302](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f2d92da8-f784-4fe7-9f75-37558abab8b7)
w is the window size.
