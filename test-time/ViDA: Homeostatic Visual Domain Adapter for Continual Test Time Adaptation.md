ViDA: Homeostatic Visual Domain Adapter for Continual Test Time Adaptation
- Continual TTA
- Motivated by noisy pseudo-label and changing distribution shift
- Using mean-teacher model

Intuitions:
- low rank adaptor effectively mitigates inter-domain divergence
- ![1701320570972](https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/dbecc299-ea49-47cb-a7bd-02a1614297ff)
- However, high rank adaptor shows more about intra-class fearure aggregation, as the above figure shows. (This figure calculate the H divergence of each domains)
- The proposed method could achieve lower distance for both inter-domain and intra-class distances.
