## [Domain Alignment Meets Fully Test-Time Adaptation](https://arxiv.org/abs/2207.04185#:~:text=A%20foundational%20requirement%20of%20a,domains%20using%20only%20unlabeled%20data.)

ACML 2023

### Introduction and background
- xxx
- xxx
- xxx

### Method
<img width=600 alt="1685324855443" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cd68ce6a-9c67-4988-9abd-cdb83b48224d">

The basic idea is rather than directly access the source data, we use PCA to reduce the source feature size and keep these features during target adaptation. We then do the same PCA for target data and then do deep alignment. During the adaptation process, we keep the classifier frozen and only update the BN in encoder.

<img width=600 alt="1685325242180" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/941d4293-7bd6-473c-8b97-cfbbe6652efc">

(2): $\Phi^*=\left(\mathrm{W}_t\right)^{\top} \mathrm{W}_s$

is a approximation where $\Phi$ is the transformation matrix that align $W_s$ and $W_t$ by

$\Phi^*=\underset{\Phi}{\arg \min }\left\|\mathrm{W}_t \Phi-\mathrm{W}_s\right\|_F^2$.

(6): <img width=200 alt="1685325723950" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9a46110b-68e7-460a-a523-d899fafc3ac1">

where A is the subspace alignment using fully connect layer of d neurons without non-linear activation function.

(7): <img width=250 alt="1685326597174" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7aa20492-d842-4db3-9e32-1f1c65a20f92">

where 
<img width=600 alt="1685326766055" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/bee15b49-b8bf-4f35-88e3-487df8d7c66e">

<img width=400 alt="1685326791034" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/fc179d5c-6bb3-4336-ae78-02622f573937">

and CB is a class-balance loss implemented as the binary cross-entropy between the
mean prediction from the network over a mini-batch and an uniform prior distribution.

### Experiments

<img width=600 alt="1685327242362" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/df7b6c3b-6d3b-4e30-b8b4-5a334ecfbe79">


### Notes
