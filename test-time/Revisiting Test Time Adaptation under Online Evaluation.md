## [Revisiting Test Time Adaptation under Online Evaluation](https://arxiv.org/abs/2304.04795)


### Introduction and background
- Current evaluation protocols overlook the effect of this extra computation cost, affecting their real-world applicability.
- To address this issue, we propose a more realistic evaluation protocol for TTA methods where data is received online from a constant-speed data stream, thereby accounting for the method’s adaptation speed.
### Method
  <img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/411d44db-4b4d-4bb1-a7d8-fe7bb541fcfd">

- Offline: only update the one who faces the time step. Otherwise, output the prediction without updating the parameter.

  <img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7f2a970b-6ec7-406b-a81f-2bd3abadec53">

- Online: measure the speed of the method processing data x as R; R will join the speed measuring process. (because some methods process data depending on the data itself, the time to process each piece of data is different.)
### Experiments
<img width=700 alt="a5" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/670f80d0-ca9d-4209-97f2-a08936ce008e">

- ImageNet-C/R/3DCC
### Notes
