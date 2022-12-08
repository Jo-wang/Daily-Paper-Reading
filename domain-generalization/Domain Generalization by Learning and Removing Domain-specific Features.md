## [Domain Generalization by Learning and Removing Domain-specific Features](https://openreview.net/pdf?id=37Rf7BTAtAM)
NeurIPS 2022   
Ranking: 3
### Introduction and background
- The features learned by the DNNs may only belong to specific domains and are not generalized for other domains. 
- a CNN that uses textures to discriminate objects in the photos has poor performance when it is applied to the sketches
- The setting of this paper is multi-source DG
- Previous methods do not clearly inform the domain-specific features should be removed, and CNN tends to learn domain-specific knowledge.
- propose a novel framework: Learning and Removing Domain-specific features for Generalization (LRDG)

### Method
- Model includes: a domain-specific classifiers, an encoder-decoder network, and a domaininvariant classifier
- Training process:
  - 1. learn domain-sepcific classifier for each source domain (the classifier cannot discriminate other domains' data)
  - 2. map the input image into new space by encoder-decoder net (domain-specific are removed by domain-sepcific classifier, so the classifier will not discriminate the classes in corresponding domain after mapping). the domain-invariant classifier will be better guided to learn the domain-invariant features.
  
 ![1670455319656](https://user-images.githubusercontent.com/46414159/206318487-635c4dda-820b-4cb1-8b79-41c8802191af.png)

- **Domain-specific feature learning**:
Learn a classifier $F_{i}$ for domain $D_{s}^{i}$ by ![image](https://user-images.githubusercontent.com/46414159/206320380-a3f25a3f-6a27-4a57-bc18-9d7798285945.png)
and max the uncertain loss on the remaining domains:
![image](https://user-images.githubusercontent.com/46414159/206320478-5e2149b8-775a-41ee-a70e-5659af3c5e15.png)
where the uncertain loss is entropy loss:
![image](https://user-images.githubusercontent.com/46414159/206320596-39c5d202-02bf-4c8f-a6e8-1440a7a91aa7.png)

- **Removing domain-specific features**:
Input image into encoder-decoder net M, map the image into new space Z, and then connect to domain-specific $F_{s}$ and domain-invariant classifier $F$.

Max uncertain loss for corresponding domain-specific classifier ($F_{s}$ are frozen) to train M:
![image](https://user-images.githubusercontent.com/46414159/206322979-8b4d0aca-d604-43f8-a468-7258637021ac.png)  
To remain the smilarity between input img and output img, use reconstruct loss (pixel-wise l2 loss):
![image](https://user-images.githubusercontent.com/46414159/206323130-584d1745-1f3a-4f34-b190-75eaa8ff4ea3.png)  
Train the domain-invariant classifier F by minimizing the classification loss $L_{C}^{FM}$ on the output images of all the source domains:
![image](https://user-images.githubusercontent.com/46414159/206323354-8beadfd7-933e-475c-82cc-7429487dcb11.png)

- **Overall**: train domain-specific: ![image](https://user-images.githubusercontent.com/46414159/206323524-41b9b8c9-4b81-4e19-9979-aee2f97ebe15.png)

learn domain-invariant: ![image](https://user-images.githubusercontent.com/46414159/206323602-6f58213b-f4e7-420b-ab24-af683fb43a96.png)




### Experiments
- Dataset: PACS, OfficeHome, VLCS
- Arch: U-net for encoder-decoder net, AlexNet ResNet18 and ResNet50 as backbones for classifiers
![1670457928176](https://user-images.githubusercontent.com/46414159/206323877-c9fd67f8-41b4-4bea-be7f-2e8c1773f884.png)
![1670458043535](https://user-images.githubusercontent.com/46414159/206324172-64c175ec-a2d4-452f-ac66-339b608fad4a.png)


### Notes
