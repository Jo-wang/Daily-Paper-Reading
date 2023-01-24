## [ACE: Ally Complementary Experts for Solving Long-Tailed Recognition in One-Shot](https://arxiv.org/abs/2108.02385)

ICCV2021 

⭐ ⭐ ⭐ ⭐


### Introduction and background
- Previously exist 3 types of framework to solve long-tailed problem:
  - one stage: re-balancing, including re-sampling and re-weighting; 🙅: accuracy of majority classes is sacrificed, indicating the under-representation of the heads
  - two stage with pretraining: firstly train the feature extractor (backbone) with the whole imbalanced set for generalizable representation learning, then re-adjust the classifier by re-sampled data or build diverse experts for various tasks in cascading stages; 🙅: heavily relying on the well-adjusted pretrained model and re-balancing skills make the frameworks sensitive to hyper-parameters and hard to find a sweet point. the accumulated training steps make the multi-stage models redundant and less practical to be integrated with other tasks simultaneously, e.g., detection and segmentation.
  - multi-stage multiexpert frameworks

- Inspiration: design a group of experts with complementary skills
  - (1) they share elementary knowledge from the most diverse data source; 
  - (2) they are professional at splits of data respectively, and aware of what they do not specialize in; 
  - (3) opinions from the experienced experts (who see more data) are incorporated to complement the judgment from junior experts (who see less) for optimal decision.

### Method
<img width="900" alt="1674478778054" src="https://user-images.githubusercontent.com/46414159/214045848-c70cec05-4f18-4215-be01-b793a7a769e1.png">

**The overall framework is defined as:**

- Shared backbone;
- distribution-aware planner distributes diverse but overlapping category splits for each expert, including target categories (TC) and interfering categories (IC);
- multiple experts (individual learnable blocks and a prediction layer);
- distribution-adaptive optimizer is designed to guide the experts to update at their own paces;
- predictions from the experts are aggregated by averaging
over the re-scaled logits in each data split

#### Distribution-aware planner

### Experiments

### Notes
