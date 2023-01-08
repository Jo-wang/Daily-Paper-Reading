## [Model Adaptation: Historical Contrastive Learning for Unsupervised Domain Adaptation without Source Data](https://arxiv.org/abs/2110.03374)

NeurIPS2021

Ranking: ⭐ ⭐ ⭐ ⭐

### Introduction and background
<img width="500" alt="Screen Shot 2023-01-08 at 23 43 20" src="https://user-images.githubusercontent.com/46414159/211199347-737b2284-e5aa-4273-9532-efbb76751930.png">

- This paper is mainly focusing on unsupervised model adaptation (another name of source-free DA ❓) to adapt source-trained models to ﬁt target data distribution without accessing the source-domain data.
- This setting alleviates the concern of data privacy and intellectual property effectively.
- More challenging and susceptible to collapse.
- Tested on image classification, semantic segmentation and object detection.

### Method
⚖️ **Comparison between UDA and UMA**   
<img width="800" alt="Screen Shot 2023-01-08 at 23 47 21" src="https://user-images.githubusercontent.com/46414159/211199525-5f782ba5-fdf8-45f8-aef3-a277f365043b.png">

🔄 **Model framework**   
<img width="800" alt="Screen Shot 2023-01-08 at 23 55 22" src="https://user-images.githubusercontent.com/46414159/211199993-197c0ae3-ebab-4fd6-a537-869efd80b09b.png">

#### Historical Contrastive Instance Discrimination (HCID)

#### Historical Contrastive Category Discrimination (HCCD)

### Experiments
- Semantic Segmentation
  - Deeplab-v2
  - GTA5 ➡️ Cityscapes, Synthia ➡️ Cityscapes
  - <img width="600" alt="Screen Shot 2023-01-08 at 23 59 10" src="https://user-images.githubusercontent.com/46414159/211200189-c89d192c-36a1-49cf-9090-b3e34efeaf15.png">
- Image Classification
  - ResNet-101 and ResNet-50
  - VisDA17 and Ofﬁce-31
  - <img width="600" alt="Screen Shot 2023-01-09 at 00 01 35" src="https://user-images.githubusercontent.com/46414159/211200309-279cdc75-a846-4add-9c77-68218aeccea0.png">
- Object Detection
  - Faster R-CNN
  - Cityscapes ➡️ Foggy Cityscapes, Cityscapes ➡️ BDD100k
  - <img width="600" alt="Screen Shot 2023-01-09 at 00 03 33" src="https://user-images.githubusercontent.com/46414159/211200425-736e743c-a0cd-4c2c-95f7-8e94f604c2f8.png">


### Notes
- t-SNE on GTA5 ➡️ Cityscapes
- <img width="650" alt="Screen Shot 2023-01-09 at 00 04 40" src="https://user-images.githubusercontent.com/46414159/211200498-fa2a71ef-d0a9-4295-bec8-e907e3e3106b.png">
