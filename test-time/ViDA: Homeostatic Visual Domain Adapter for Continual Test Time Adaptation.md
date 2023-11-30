ViDA: Homeostatic Visual Domain Adapter for Continual Test Time Adaptation
- Continual TTA
- Motivated by noisy pseudo-label and changing distribution shift
- Using mean-teacher model

Intuitions:
- low rank adaptor effectively mitigates inter-domain divergence
- ![1701320570972](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/dbecc299-ea49-47cb-a7bd-02a1614297ff)
- However, high rank adaptor shows more about intra-class fearure aggregation, as the above figure shows. (This figure calculate the H divergence of each domains)
- The proposed method could achieve lower distance for both inter-domain and intra-class distances.

- This ViDA could make low-rank adaptor focusing more on foreground while somewhat disregard the background, as the below image shows
- ![1701321134550](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/2c9b32f8-36bf-4454-895c-fda30c89a36c)
- High rank adaptor better suited to address error accumulation in the continual adaptation process, as the below image shows.
- ![51f45b812fa8fffb35d056706e16a25](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/f5656ea8-1807-4407-9b54-4c52ac5a5203)


