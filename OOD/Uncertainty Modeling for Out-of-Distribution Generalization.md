## [Uncertainty Modeling for Out-of-Distribution Generalization](https://arxiv.org/abs/2202.03958)

ICLR2022

Ranking: :star: :star: :star: :star:

### Introduction and background
- Previous work say feature statistics (mean and standard deviation) **carry informative domain characteristics** of the training data.
- :star: To define domain characteristic: the information that is more specific to the individual domains but less relevant to the task objectives.
- Consequently, domains with different data distributions generally have inconsistent feature statistics 
- Uncertain statistics shifts: 
![1672794785819](https://user-images.githubusercontent.com/46414159/210466607-01cdff7b-b595-4575-b0f6-cdf065effb9c.png)
- Previous methods are mainly linear manipulation on pairwise samples to generate new feature statistics. (sub-optimal)
- In this paper, to improve the generalization ability, they are trying to properly modeling **Domain Shifts with Uncertainty (DSU)**, i.e., characterizing the feature statistics as uncertain distributions.

### Method
- Preliminaries: intermediate feature $x$, channel-wise mean $\mu$, and std $\sigma$
![1672795784429](https://user-images.githubusercontent.com/46414159/210467966-7767b4bf-c712-4400-96fd-4a9679c381e1.png)
![1672803285549](https://user-images.githubusercontent.com/46414159/210479828-0dcf512e-6417-4e5f-a37f-f7e76cb2d2f8.png)

- To model the domain shift by uncertainty, we assume the distribution of each feature statistic follows a multi-variate Gaussian distribution. Mean: $N(\mu, \Sigma_{\mu}^{2})$, and std $N(\sigma, \Sigma_{\sigma}^{2})$

- To estimate the uncertainty, we can calculate the batch-wise uncertainty by:   

  - $\Sigma_\mu^2(x)=\frac{1}{B} \sum \left(\mu(x)-\mathbb{E}_b[\mu(x)]\right)^2$     

  - $\Sigma_\sigma^2(x)=\frac{1}{B} \sum \left(\sigma(x)-\mathbb{E}_b[\sigma(x)]\right)^2$, 
where $\sum$ is the uncertainty estimation of mean $\mu$ and std $\sigma$

- after get the distribution of the statistics, we can use random sample: mean $\beta (x) \sim N(\mu, \Sigma _{\mu}^{2})$, and std $\gamma (x) \sim N(\sigma, \Sigma _{\sigma}^{2})$
  - $\beta(x)=\mu(x)+\epsilon_\mu \Sigma_\mu(x), \quad \epsilon_\mu \sim \mathcal{N}(\mathbf{0}, \mathbf{1})$
  - $\gamma(x)=\sigma(x)+\epsilon_\sigma \Sigma_\sigma(x), \quad \epsilon_\sigma \sim \mathcal{N}(\mathbf{0}, \mathbf{1})$
- The final form is:
![image](https://user-images.githubusercontent.com/46414159/210482954-a1160c44-10e5-4e9e-bffa-829a718faa63.png)

### Experiments
#### Classification
- Setup: 
  - PACS (single domain), with MixStyle (leave-one-out + ResNet18)
  - OfficeHome (multi-domain)
- exp:   
![1672805646268](https://user-images.githubusercontent.com/46414159/210483384-9d2707a3-0006-418d-80eb-1769514d8ae2.png)
![1672807619460](https://user-images.githubusercontent.com/46414159/210486343-371a1a97-c01f-47b8-8e48-3feb83bdf07e.png)

#### Semantic Segmentation
- Setup: GTA5 $\Rightarrow$ Cityscapes, FADA code with DeepLab-v2 (ResNet101)
- exp:   
![1672805951295](https://user-images.githubusercontent.com/46414159/210483888-53610b8a-2886-4909-af69-3b118004292c.png)

#### Instance Retrieval & Robustness (see the paper for details)

### Ablation Study
- Inserted position (ConvBlock position)
![1672807248114](https://user-images.githubusercontent.com/46414159/210485773-8f8ddc3d-9f49-4e92-aef9-e3a73c8ab4af.png)

- Hyper-parameter 
  - (probability $p$ om algorithm 1)
![1672807266043](https://user-images.githubusercontent.com/46414159/210485804-ff572ee4-c3cc-4208-a343-4bb0d657f1e9.png)
  - Batch size
![1672807473768](https://user-images.githubusercontent.com/46414159/210486111-a72ed558-fd02-44e5-b038-7ef599995515.png)

- Uncertainty Distribution
![1672807288502](https://user-images.githubusercontent.com/46414159/210485832-dc693246-86f0-4a0f-b33f-0101f927fc33.png)

**See the Appendix.3 for more choices of uncertainty distribution**

![1672807383701](https://user-images.githubusercontent.com/46414159/210485980-4daa69a0-9267-475c-a5b5-fd667640a88d.png)

### Baseline
#### Domain generalization with mixstyle (ICLR2021)
- 1. Instance Normalization: $\operatorname{IN}(x)=\gamma \frac{x-\mu(x)}{\sigma(x)}+\beta$, where $\gamma$ and $\beta$ are learnable affine transformation parameter, $\mu (x)$ and $\sigma (x)$ are mean and std across the spatial dim within each channel.    
![1672809905680](https://user-images.githubusercontent.com/46414159/210489847-6b321363-7729-4314-bf0a-bba33441e5fe.png)
- 2. AdaIN changes $\gamma$ and $\beta$ in **IN** to $\sigma (y)$ and $\mu (y)$ to achieve arbitrary style transfer: $\operatorname{AdaIN}(x)=\sigma(y) \frac{x-\mu(x)}{\sigma(x)}+\mu(y)$.
- 3. MixStyle: mixes the feature statistics of two
instances with a random convex weight to simulate new styles.
  - Generate a reference batch $\tilde{x}$ from $x$. If $i$ and $j$ represent differnet domain, shuffle the position of $x_{i}$ and $x_{j}$, **if domain label not available**, shuffle $x$ as Fig.(b): 
  ![1672810526536](https://user-images.githubusercontent.com/46414159/210490824-0eb56260-b662-4e2b-8b2a-c3e28c6e2061.png)
  - Compute the mixed feature statistics:
  $\gamma_{\operatorname{mix}}=\lambda \sigma(x)+(1-\lambda) \sigma(\tilde{x})$       
  $\beta_{\text {mix }}=\lambda \mu(x)+(1-\lambda) \mu(\tilde{x})$, where $\lambda$ is instance-wise weights sampled from Beta Distribution $\lambda \sim Beta(\alpha, \alpha)$, and $\alpha=0.1$ is a hyper-parameter.
  - Then we have: $\operatorname{MixStyle}(x)=\gamma_{m i x} \frac{x-\mu(x)}{\sigma(x)}+\beta_{m i x}$
![1672811671780](https://user-images.githubusercontent.com/46414159/210492812-d11b8036-1471-4f5f-b90c-d568ab61fbda.png)

### Notes
This method can be flexibly used in image classification or segmentation tasks as a trick.
