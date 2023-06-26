## [Evaluating Continual Test-Time Adaptation for Contextual and Semantic Domain Shifts](https://arxiv.org/pdf/2208.08767.pdf)


### Introduction and background
- **Contextual shifts** correspond to the types of environments; for example, a model pre-trained in an indoor context has to adapt to the outdoor context on CORe-50.
- **Semantic shifts** correspond to the capture types; for example, a model pre-trained on natural images has to adapt to clipart, sketches, and paintings on DomainNet.
- Conclusion:
  - i) Test-time adaptation methods perform better and forget less about contextual shifts compared to semantic shifts
  - ii) TENT outperforms other methods on short-term adaptation, whereas CoTTA outperforms other methods on long-term adaptation
  - iii) BN is the most reliable and robust

### Method
- **Forget Rate**: the difference in accuracy before and after continually adapting to the target domains.

#### Effect of Batch Size

<img width=600 alt="q" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/9ac26481-da44-49fa-af80-e48170040d6e">
    
#### Test for Short-term adaptation: contextual shift
- Can only see the test sample once
- Default train domains -> default test domains:
          
  <img width=600 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/023e61b1-622e-4bea-9493-e738cacd24a8">
     
- Outdoor -> indoor:
     
  <img width=600 alt="adf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/60dc879a-2001-4db0-9621-5f85dc02433e">
    
- Single domain -> all other domains:
    
  <img width=600 alt="afdf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/8ebc85a6-2461-4088-9061-14e51bd4b43a">
     
#### Test for Short-term adaptation: semantic shift
- Can only see the test sample once
- Real images -> paintings, clipart and sketches:
        
  <img width=600 alt="afddf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/1477c8a5-1afc-46cb-bdb7-5482cf210024">
      
- Paintings -> real images, cliparts and sketches:
       
  <img width=600 alt="affeddf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/ca019bfb-9a93-4461-ac94-21341940a49c">

#### Test for Long-term adaptation
- can see the test sample multiple times.
<img width=600 alt="affecdddf" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/cb55315b-0498-4433-94eb-60b4b4e5a0c3">

### Experiment setting
- 3 seeds
- BS=128
- ResNet-50
- Pretrained on ImageNet-1k
- See paper for dataset train/val/test segmentation.

### Note
Didn't include too many paper
