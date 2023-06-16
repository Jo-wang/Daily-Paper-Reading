## [Learning to Adapt to Online Streams with Distribution Shifts](https://arxiv.org/abs/2303.01630)

2023


### Method
<img width=400 alt="a" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/5df9c898-233d-4cd5-9b35-6e7062ce6b00">
         
<img width=700 alt="a2" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/7dbecdb3-a080-4ba5-9356-001d14fdb6b0">

- Uses MAML way to apply meta-learning to TTA.
- Customize the source pretraining process a lot.

<img width=400 alt="a23" src="https://github.com/Jo-wang/Daily-Paper-Reading/assets/46414159/37fc036c-8676-4228-8de2-41db5e3d1ef2">

- First sample source in a stream of data and update the model for self-supervised learning (rotation prediction) in the inner loop. 
- Outer loop: (sample K samples for D domains and 1 for D' domains, on total N = KD + D') update the network from learned feature extractor $w_L$ and init classifer $\phi_0$ by CE.
- Uses learned feature extractor by both inner and outer loop + learned self-supervised head at inner loop + learned classifier (at outer loop) to do TTA.
- Update TTA model in the inner loop manner. Update on feature extractor and self-supervised head, then use feature extractor (updated by test data) classification head (not updated by test data) to make the prediction.
### Experiments

### Notes
