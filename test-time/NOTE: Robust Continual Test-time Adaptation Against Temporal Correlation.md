## [NOTE: Robust Continual Test-time Adaptation Against Temporal Correlation](https://arxiv.org/abs/2208.05117)

NeurIPS2022

Code: https://github.com/TaesikGong/NOTE

**Main Task:** present a new test-time adaptation scheme that is robust against non-i.i.d.
test data streams (with the time t changes)

### Introduction and background
- performance degrades under distributional shifts between the training data and test data
- previous work assume ($x_t, y_t$) i.i.d. drawn from $P_T (x,y)$
- However, the distribution of online test samples often changes across the time axis, i.e., ($x_t, y_t$) ∼ $P_T (x,y|t)$ in many applications
- naïvely adapting to the incoming batch of test samples could be problematic for both approaches: the batch is now more likely to (a) remove instance-wise variations that are actually useful to predict y, i.e., the “contents” rather than “styles” through normalization, and (b) include a bias in p(y) rather than uniform

<img width=350 alt="1680673077780" src="https://user-images.githubusercontent.com/46414159/229990392-28dad764-6ae9-4f56-9949-38542ce6e07c.png">

- the existing model might be biased towards these imbalanced samples under the temporally correlated test streams

### Method
<img width=700 alt="1680675666328" src="https://user-images.githubusercontent.com/46414159/229997525-d038bca2-9e9f-4bca-9568-d964ba704b9e.png">

#### Instance-Aware Batch Normalization
**Problem:** assume feature map $\mathbf{f} \in \mathbb{R}^{B \times C \times L}$, given a feature map $\mathbf{f}_{:, c,:}$ by the stats $\hat{\boldsymbol{\mu}}_c, \hat{\boldsymbol{\sigma}}_c^2$ computed across B and L is expected that **averaging information across B can marginalize out uninformative instance-wise variations for predicting y**. **But under temporal correlation in B, this assumption no longer hold.**

**To solve it:**  propose correcting normalization statistics on a per-sample basis.
- Do not directly switch the BN stats into new, but consider instance-wise stats $\tilde{\boldsymbol{\mu}}, \tilde{\boldsymbol{\sigma}}^2 \in \mathbb{R}^{B, C}$ of f (like IN)
- <img width=700 alt="1680677631983" src="https://user-images.githubusercontent.com/46414159/230003732-45f9743e-0485-452d-87fd-c315db35dfea.png">
- means if the new mean and variance is very different from org ones by the $\alpha$*variance(of new stats), we will modify the stats. A high value of $\alpha$ relies more on the learned statistics (BN), while a low value of $\alpha$ is in favor of the current statistics measured from the instance. 
- So, the output of the new IABN is:
- <img width=400 alt="1680678181145" src="https://user-images.githubusercontent.com/46414159/230005550-3954bde5-b8b8-4475-ba63-d92c10adc4a7.png">
- when $\alpha$ is 0, this is IN and when it turns infinity, this is BN.

#### Adaptation via Prediction-Balanced Reservoir Sampling
**Problem:** Temporally correlated distributions lead to an bias in p(y).

<img width=700 alt="1680678702191" src="https://user-images.githubusercontent.com/46414159/230007399-1362c9e9-198b-468c-8143-3972697c540b.png">

**To solve it:** mimics i.i.d. samples from temporally correlated streams with the assistance of a small (e.g., a mini-batch size) memory.

- Time-uniform sampling: reservoir sampling (RS) collect time-uniform data in a
single pass on a stream without prior knowledge of the total length of data
- Prediction-uniform sampling: use the predicted labels to compute the majority class(es) in the memory. We then replace a random instance of the majority class(es) with a new sample.

- To avoid performance degraded if there's severe shift, uses EMA to update $\mu _t$ and   $\sigma _t$ from previous step (t-1) by the memory. e.g., $\mu _t=(1-m) \mu _{t-1}+m \frac{N}{N-1} \hat{\mu}_t$

#### Inference   
<img width=700 alt="1680679336207" src="https://user-images.githubusercontent.com/46414159/230009929-66460a1c-ad5f-4a90-8724-2bf40ec0be42.png">

### Experiments
- dataset: CIFAR10-C, CIFAR100-C, and ImageNet-C 
- exp:
<img width=700 alt="1680679486733" src="https://user-images.githubusercontent.com/46414159/230010577-6f02ef54-84f2-483b-bef3-c1b033e92cd7.png">

<img width=700 alt="1680679621688" src="https://user-images.githubusercontent.com/46414159/230011097-1ccc02ad-6730-4fe4-83d2-724627574c0a.png">

- Ablation:
<img width=700 alt="1680679653301" src="https://user-images.githubusercontent.com/46414159/230011212-daa8afdd-18be-4d53-94cf-c9f41904de6d.png">


### Notes
