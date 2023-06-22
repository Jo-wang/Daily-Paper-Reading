## [Revisiting Test Time Adaptation under Online Evaluation](https://arxiv.org/abs/2304.04795)


### Introduction and background
- Current evaluation protocols overlook the effect of this extra computation cost, affecting their real-world applicability.
- To address this issue, we propose a more realistic evaluation protocol for TTA methods where data is received online from a constant-speed data stream, thereby accounting for the method’s adaptation speed.
### Method
- Offline: only update the one face the time step. (otherwise, just output the prediction without updating the parameter)
- Online: measure the speed of method processing data x as R, R will join the speed measuring process. (because some methods process data depends on the data itself, so the time to process each data is different)
### Experiments

### Notes
