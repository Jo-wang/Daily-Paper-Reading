## [A Simple Test-time Adaptation Method for Source-free Domain Generalization](https://openreview.net/pdf?id=Ran2xUWG2n)

ICLR2023



### Method
<img width=700 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7b4b0eed-67db-4489-8f17-26d6b4c3da44">

<img width=700 alt="aa" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6c5f9848-061b-48f9-82bc-1d82a98d96b4">

- Multiple sources, each source has a model -> **kind of no source modification**
- **Kind of online adaptation** (get plabel -> CE to update all source models -> get new pseudo label)

### Experiments
- VLCS, PACS, OfficeHome, TerraIncognita.
- ResNet-50
- incremental/episodic/non-episodic
