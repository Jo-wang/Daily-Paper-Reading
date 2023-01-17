## [Source-Free Adaptation to Measurement Shift via Bottom-Up Feature Restoration](https://arxiv.org/pdf/2107.05446.pdf)

ICLR2022

Ranking: :star: :star: :star: :star:

### Introduction and background
- Current source-free mainly focusing on classification; destroy model calibration; and target has well-separated data clusters.
- But even the most innocuous of shifts can destroy this initial feature-space class-separation in the target domain, and with it, the performance of these techniques
- This paper defined measurement shift: characterized by a change in measurement system and is particularly pervasive in real-world deployed machine learning systems. For example, different scanner in medical image segmentation. **Under this shift, restoring the source features in the target domain is sufficient to restore performance.** (物體本身沒有variance，只是觀測物體的環境出現variance，這種情況比較局限)
- :star2: Mainly focusing on: 
  - measurement shift; 
  - new method that softly-binned historigams approx the marginal feature distributions; 
  - outperform SFDA in terms of acc, calibration, and data efficiency; 
  - talk about the issues of entropy minimization methods.

### Method
<img width="400" alt="1673916946838" src="https://user-images.githubusercontent.com/46414159/212787043-ce17fc36-0744-43ea-b165-e19e34fcf4af.png">

- Define the domain shift: $L$ is domain-invariant latent representation; $E$ is domain (or environment) variable; $m$ is domain-dependent mapping.

- Setting: source-free, but the lightweight source statistics $S_s$ at target adaptation time (development time) is available.

<img width="700" alt="1673920507876" src="https://user-images.githubusercontent.com/46414159/212792805-7a45ec3e-83b6-49a9-b69f-5768722d1899.png">

#### Development
- Normal source pre-training. The model contains feature extractor $g$ and classifier $h$. While $h$ is frozen when adapt to target.
- Use soft binning function to store the source statistics:
<img width="800" alt="1673918000586" src="https://user-images.githubusercontent.com/46414159/212788515-dea72c5d-f94d-4cee-bd51-219dfdd82908.png">
<img width="800" alt="1673918028332" src="https://user-images.githubusercontent.com/46414159/212788558-642d6911-fb02-4cfb-abb2-49280be22238.png">
Details:
<img width="800" alt="1673919039440" src="https://user-images.githubusercontent.com/46414159/212790360-40e6f75f-900f-4116-b8e8-a64b677a9c40.png">



#### Deployment
<img width="800" alt="1673920583660" src="https://user-images.githubusercontent.com/46414159/212792959-d90a939b-07f0-4b9c-84f4-87ea6bfc55dc.png">

#### Bottom-Up Feature Restoration (BUFR) :star:
Adapt $g_t$ (target feature extractor) in a bottom-up manner, training for several epochs on one “block” before “unfreezing” the next. Here, a block can represent a single layer or group of layers.

### Experiments
- dataset: create a new dataset EMNIST-DA (based on the 47-class Extended
MNIST (EMNIST) character-recognition dataset);  CIFAR-10-C and CIFAR-100-C; CAMELYON17

### Notes
Soft-binning origional paper:
<img width="350" alt="1673918831899" src="https://user-images.githubusercontent.com/46414159/212789925-e94beeeb-e776-4b54-a8cf-76ba9c6c089d.png">
