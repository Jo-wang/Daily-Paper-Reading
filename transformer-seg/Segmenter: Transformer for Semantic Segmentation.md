## [Segmenter: Transformer for Semantic Segmentation](https://openaccess.thecvf.com/content/ICCV2021/papers/Strudel_Segmenter_Transformer_for_Semantic_Segmentation_ICCV_2021_paper.pdf)

ICCV2021

Ranking: 4



### Introduction and background
- Conventional CNN-based methods has context-local intersaction trade off.
![1671767208772](https://user-images.githubusercontent.com/46414159/209267083-e74d09eb-7d1f-4306-a3ec-9527a78905f3.png)

### Method
![1671767261638](https://user-images.githubusercontent.com/46414159/209267177-1c485e3a-ffd6-4116-9735-63bd49bb775d.png)

![image](https://user-images.githubusercontent.com/46414159/210195538-820719aa-d387-4b39-92bc-c548ae5b2958.png)

#### Encoder
<img width="1250" alt="Screen Shot 2023-01-02 at 14 42 21" src="https://user-images.githubusercontent.com/46414159/210195699-12ac35ed-48e9-4f24-8015-1c1531f65299.png">

#### Decoder
<img width="1250" alt="Screen Shot 2023-01-02 at 14 43 16" src="https://user-images.githubusercontent.com/46414159/210195753-e1f6515b-bd53-497c-9dbe-563ec0a439c4.png">

### Experiments
- Dataset: ADE20K, Pascal Context, Cityscapes
- Pre-exp 
<img width="600" alt="Screen Shot 2023-01-02 at 16 34 27" src="https://user-images.githubusercontent.com/46414159/210200727-e244a97d-b842-4355-a34e-41e3dc047d02.png">
- exp
<img width="1200" alt="Screen Shot 2023-01-02 at 16 38 40" src="https://user-images.githubusercontent.com/46414159/210200989-6d967ce4-df32-4c1c-99f4-b6cb5e0873ba.png">
<img width="680" alt="Screen Shot 2023-01-02 at 16 39 36" src="https://user-images.githubusercontent.com/46414159/210201045-8d0ac7a9-9fac-45ee-a805-e3646d9fc489.png">

<img width="700" alt="Screen Shot 2023-01-02 at 16 35 49" src="https://user-images.githubusercontent.com/46414159/210200803-eda9b161-2f6f-4fda-a915-90750b859b93.png">

### Notes
For the details of ViT, see https://github.com/wangshusen/DeepLearning/blob/master/Slides/10_ViT.pdf
