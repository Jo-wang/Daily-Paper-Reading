## [Domain Generalization by Learning and Removing Domain-specific Features](https://openreview.net/pdf?id=37Rf7BTAtAM)
NeurIPS 2022

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

  
### Experiments

### Notes
