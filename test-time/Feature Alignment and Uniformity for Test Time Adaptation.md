## [Feature Alignment and Uniformity for Test Time Adaptation](https://arxiv.org/pdf/2303.10902.pdf)

CVPR2023


### Method
- Source $D_s$, target $D_t$, model $g = f \cdot h$, where $f$ is backbone and $h$ is linear classifier; image embedding $z_i = f(x_i)$, logits $p_i = h(z_i)$

- Create a memory bank $\mathcal{B}$ to save each $(z_i, p_i)$ for sample $x_i$
- For each class $k$, top $M$ highest entropy in the memory bank will be ignored in order to calculate the prototype: <img width=120 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f53295cd-5012-47a1-9cc3-35bcb4c35ba5">

- Then we get the prototype-based classification output: <img width=140 alt="a1" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/58ef7193-88e3-4af6-bf46-cbf1fa698224">

  $sim(\cdot)$ is the cosine similarity between feature $z$ and prototype $c$.

- According to the assumption that the prototype-based classification results $y_i$ and outputs $p_i$ of the network $g$ should share a similar distribution for the same input, we use loss: $\mathcal{L}_i\left(p_i, y_i\right)=-\sigma\left(p_i\right) \log y_i$, where $\sigma$ is the softmax operation.
- But there's still mistake prediction, so we use consistency filter: $\mathcal{M}_i=\mathbb{1}\[ \arg \max p_i=\arg \max y_i \]$, this is a mask and the value could be $1$ only the prediction is consistency.

  $\mathcal{L}_{t s d}=\frac{\sum_i \mathcal{L}_i * \mathcal{M}_i}{\sum_i \mathcal{M}_i}$

- encourage K-nearest neighborhood features instead of all the features to be close to reducing the noisy label impact:
  - concatenate spatial local clustering with the memory bank
  - retrieving K-nearest features in the memory bank for image $x$
  - the logits of image $x$ should be aligned with the logits of its nearest neighbors in the latent space
  
  - <img width=240 alt="a2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/efa868d8-98bc-4104-9031-9ad6bcccaeec">
  
    <img width=40 alt="a223" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2c16ae51-bc7e-4b3c-bd08-8cb96c79cbc3"> is the k-nearest embedding of $z$ in memory bank. If feature is close (sim() is large), make the logits close more. sim().detach() make the sim() as a constant.
    
### Experiments
- PACS, VLCS, DomainNet, OfficeHome, CIFAR10C/100C, ImageNet-C, medical image segmentation
