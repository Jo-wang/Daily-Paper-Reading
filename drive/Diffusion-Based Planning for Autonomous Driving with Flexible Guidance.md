## [Diffusion-Based Planning for Autonomous Driving with Flexible Guidance](https://openreview.net/forum?id=wM2sfVgMDH)

ICLR 2025

Ranking: 3

### Introduction and background
- Human drivers exhibit multi-modal behaviors, but behavior cloning struggles to model such complexity, even with large transformer models or multi-trajectory sampling.
- In out-of-distribution scenarios, directly using model outputs leads to poor planning, often requiring fallback to rule-based methods, which inherit their limitations.
- Imitation learning alone is insufficient to capture the diversity of driving behavior; using auxiliary losses to penalize unsafe plans can cause objective conflicts and fails to teach recovery from mistakes.
- Well-trained models lack adaptability, making it difficult to modify behaviors for specific requirements.

### Preliminaries

#### Autonomous Driving and Closed-Loop Planning
- Closed-loop planning is a key challenge in autonomous driving.
- Unlike open-loop planning (which assumes static conditions), closed-loop planning integrates real-time perception, prediction, and control.
- Vehicles must constantly adapt to dynamic environments (other agents, uncertain sensors, road layout), requiring precise and adaptive behavior.
- Motion prediction alone (predicting future states of agents) isn’t sufficient. Closed-loop planning implies acting in response to those predictions.

#### Diffusion Model and Guidance Schemes

(1) Diffusion Model Basics
- Based on denoising diffusion probabilistic models (DDPM).
- Forward process: progressively adds Gaussian noise to clean data over time:
$$q_{t0}(x^{(t)} | x^{(0)}) = \mathcal{N}(x^{(t)} | \alpha_t x^{(0)}, \sigma_t^2 I)$$ where $$\alpha_t = \sqrt{1 - \sigma_t^2}$$ and $$t \in [0, 1]$$
- Reverse process: denoises using a score function (gradient of log-probability):
$$dx^{(t)} = \left[f(t)x^{(t)} - \frac{1}{2}g(t)^2 \nabla_{x^{(t)}} \log q_t(x^{(t)}) \right] dt$$
with $$f(t)$$, $$g(t)$$ derived from $$\alpha_t$$, $$\sigma_t$$.
- A neural network $$s_\theta(x^{(t)}, t)$$ is trained to predict the score function $$\nabla_{x^{(t)}} \log q_t(x^{(t)})$$.

(2) Classifier Guidance
- Allows conditioning the generation process to meet certain goals (e.g., safety, comfort).
- Gradient from a classifier $$E_\phi(x^{(t)}, t)$$ is used to modify the diffusion score:
$$\tilde{s}\theta(x^{(t)}, t) = s\theta(x^{(t)}, t) - \nabla_{x^{(t)}} E_\phi(x^{(t)}, t)$$
- Compared to rule-based refinement, guidance modifies the generation internally, leveraging the model’s structure to produce high-quality, tailored results.

Intuition:
- Imagine the model wants to generate a path that might collide with another car.
- The classifier says “this path is unsafe” → high energy.
- The gradient $$\nabla_{x^{(t)}} E_\phi$$ points away from the unsafe trajectory.
- So subtract this gradient → the model shifts its output toward a safer trajectory.

Key Points:
- No retraining required — guidance is applied only at inference.
- Can be used for multi-objective planning: safety, comfort, speed control, lane keeping.
- Can combine multiple guidance terms (sum of gradients).
- Can be training-free if you approximate E using existing model outputs.


```python
# Inputs:
# - T: total number of denoising steps
# - x_T: initial noise sample
# - mu_theta(x_t, t, C): denoised output from model
# - s_theta(x_t, t): learned score function
# - compute_energy(x_0): guidance energy function(s)
# - get_alpha_sigma(t): noise schedule (returns alpha_t, sigma_t)
# - update_sample(): diffusion solver (e.g., DPM-Solver)

# Initialize
x_t = sample_gaussian_noise()  # x_T ~ N(0, I)

for t in reversed(range(1, T+1)):
    
    # 1. Compute model score
    score = s_theta(x_t, t)

    # 2. Predict denoised sample
    x_0_hat = mu_theta(x_t, t, condition=C)

    # 3. Compute energy and its gradient (guidance)
    E = compute_energy(x_0_hat)  # e.g., collision, speed, etc.
    grad_E = gradient(E, x_t)    # dE/dx_t via autograd

    # 4. Modify score using classifier guidance
    guided_score = score - grad_E

    # 5. Update sample using diffusion solver (ODE/SDE)
    x_t = update_sample(x_t, guided_score, t)

# Final output
x_0 = x_t  # Denoised trajectory sample

```

### Method
![image](https://github.com/user-attachments/assets/4bf7380c-f1e8-497c-b3c3-68948b205c78)


### Experiments

### Notes
