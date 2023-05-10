## [MM-TTA: Multi-Modal Test-Time Adaptation for 3D Semantic Segmentation](https://arxiv.org/abs/2204.12667)

CVPR2022

### Introduction and background
- There are two main issues occurred when directly using TENT to image and point cloud: 1. min ent tends to produce sharp output distribution, this may increase the cross-modal discrepancy. 2. If using consistency loss to min the discrepancy, the performance may worse due to the unavailability of the target label.
- To solve above issue, our goal is to have reliable pseudo labels
- Intra-modal Pseudo-label Generation (Intra-PG): only updating batch norm parameters by seeing the test data once. We have two branches, one is **slow modeling**, init para from source pre-trained model and momentum update the BN statistics. Another one is **fast modeling**, directly updated by the test data. Then fuse predictions from the slow-/fastupdated
statistics.
- Inter-modal Pseudo-label Refinement (Inter-PR): leverage
the Intra-PG module to measure the prediction consistencies of each modality separately, and then provide a fused prediction from slow-fast models to the Inter-PR module
- To conclude, maintain intra- and inter-modal consistency.

### Method

<img width=350 alt="1683714841389" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/dbe96fff-c5a1-4220-9463-25e006602a81">

#### Intra-modal Pseudo label Generation (similar as TENT)

For each modal:
- fast-updated model: source checkpoint, upating directly by the test data
- slow updated model: update the BN by momentum $$\lambda$$, commonly set to 0.99, so it's very slow.
- Then the prediction is the mean of these two model output (S is slow and F is fast)    
     
<img width=250 alt="1683719016210" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/c6718029-f9a2-4f5f-9e0e-2a57f051c75d">      

- plabel is the argmax of the prediction 
        
<img width=200 alt="1683719080659" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/65354ba5-04d1-4771-9748-247c15a2e3d4">

#### Inter-modal Pseudo label Refinement

<img width=350 alt="1683719249313" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/70f47879-fdb6-4542-98aa-c96585b1323d">

where Sim(.) is inverse KL divergence:

<img width=250 alt="1683719363732" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f93cd412-c1aa-487a-b303-4ff718d4e847">

- Hard select: takes each pseudo label exclusively from one of
the modalities
- Soft select: conducts a weighted sum of pseudo labels from the two modalities using the consistency measure.

<img width=350 alt="1683719615355" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/6f453bb1-7fcc-4996-934d-1071af15b582">

### Experiments
- dataset: A2D2-to-SemanticKITTI; nuScenes Day-to-Night; Synthia-to-SemanticKITTI
- arch: 2D (U-Net with a ResNet34 encoder); 3D (U-Net (downsampling 6-times) that utilizes sparse convolution on the voxelized point
cloud input, where we use either SparseConvNet or MinkowskiNet)
![1683720234329](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/edd630fd-a5bb-42f3-b14a-befd719cd330)
![1683720276674](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/93b2730e-3bf9-478f-938a-457d926b00b3)

