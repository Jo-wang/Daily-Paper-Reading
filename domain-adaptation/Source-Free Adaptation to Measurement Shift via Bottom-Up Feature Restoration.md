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
- Setting: source-free, but the lightweight source statistics $S_s$ at target adaptation time (development time) is available.

### Experiments

### Notes
