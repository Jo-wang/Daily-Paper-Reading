## [SegFormer: Simple and Efficient Design for Semantic Segmentation with Transformers](https://arxiv.org/abs/2105.15203)
NeurIPS2021

Ranking: 4
### Introduction and background
- ViT has some limitations: 1) ViT outputs single-scale low-resolution features instead of multi-scale ones. 2) It has high computation cost on large images. 
- PVT etc., these methods mainly consider the design of
the Transformer encoder, neglecting the contribution of the decoder for further improvements.
- SegFormer is:
  - A novel positional-encoding-free and hierarchical Transformer encoder.
  - A lightweight All-MLP decoder design that yields a powerful representation without complex and computationally demanding modules.

### Method
- Encoder outputs multi-scale features
- MLP decoder aggregates information from different layers

![1672720808837](https://user-images.githubusercontent.com/46414159/210300997-69aaa57d-4b33-4a48-8f9a-f68e003348e6.png)

#### Encoder
- 1. Input image divided into 4*4 patches (makes better dense prediction task)
- 2. Within the transofrmer block: 
  - Efficient Self-attention reduces the sequence to lower computational cost
  - Mixed-FFN used to implement data driven positional encoding
  - Overlap patch merging to reduce feature map size
#### Decoder
- MLP layer:
  - Features from the encoder go through MLP layer to unify in channel dimension
  - Features are upsampled to 1/4th and concat together
- MLP is adopted to fused the concated features
- MLP layer takes fused feature to predict the segmentation mask
### Experiments
![1672720021202](https://user-images.githubusercontent.com/46414159/210300076-4f26c3e0-415b-4b11-843c-98d7fcbb6216.png)
![1672722538959](https://user-images.githubusercontent.com/46414159/210302967-f5254599-640b-4657-851d-cad9f31eff96.png)

### Notes
- FLOPs: CNN 模型所需的计算力flops是什么？怎么计算？ - 阿柴本柴的文章 知乎 https://zhuanlan.zhihu.com/p/137719986
