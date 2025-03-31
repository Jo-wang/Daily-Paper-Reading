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

#### Task Redefinition

Traditionally:
- Planning = generate future trajectory for the ego vehicle.
- Prediction = forecast trajectories of nearby agents (cars, bikes, etc.)
- These are often handled separately, or with prediction treated as external input.

This paper proposes to jointly model both **Trajectory generation for: ego + M nearest neighbors**

This joint task is treated as one generative process, producing future states for all key agents conditioned on: current state, history, map, and navigation goal. This encourages cooperative interaction modeling, e.g., the ego slows down if a neighbor might cut in.

Why Use Diffusion?

Joint modeling of multiple agents is multi-modal and complex. A simple behavior cloning model:
- Can’t capture diverse futures (e.g., left vs right turn).
- Can’t model interactions well.
- Needs rule-based correction.

So, they use a diffusion model to capture the distribution over future trajectories, including uncertainty and multi-agent coordination.

1. **Formulation**
![image](https://github.com/user-attachments/assets/d7824650-db65-491b-a30b-42f1abe65ea5)

- Each x contains position and orientation (e.g., [x, y, $$\cos\theta$$, $$\sin\theta]$$)
- $$\tau$$: number of future steps
- M: number of neighbor agents

This is the target the diffusion model will generate.


2. **Training Objective (Diffusion loss)**

Train the model to recover clean trajectory $$x^{(0)}$$ from noisy version $$x^{(t)}$$, via:
![image](https://github.com/user-attachments/assets/90c7a181-cca5-4b7a-87a3-b3d38a73e484)

Where:
- $$\mu_\theta$$: predicted denoised trajectory from the model
- C: conditional inputs (scene, map, history, goal)
- $$q_{t0}$$: forward noising process
- The model learns to denoise trajectories, thus modeling the data distribution

#### Model
<img width="826" alt="Screenshot 2025-03-31 at 12 47 32 PM" src="https://github.com/user-attachments/assets/9965fa14-7065-4846-9d4e-a22ddf9f3e97" />

<img width="826" alt="Screenshot 2025-03-31 at 12 50 12 PM" src="https://github.com/user-attachments/assets/7950553a-fe0e-4296-b83a-9f4f4279f003" />

<img width="826" alt="Screenshot 2025-03-31 at 12 55 59 PM" src="https://github.com/user-attachments/assets/e42f169f-5ca6-4803-8a75-18c4c322b636" />

<img width="826" alt="Screenshot 2025-03-31 at 1 27 29 PM" src="https://github.com/user-attachments/assets/bb99173e-87e9-4fdb-a296-c5a2f32332c2" />

✅ Applicable Energy Functions

1. **Target Speed Maintenance**: Encourages the ego vehicle to maintain a desired average speed.

$$E_{\text{speed}} = \left[\max\left(\frac{\text{avg speed} - v_{\text{low}}}{1}, 0\right)^2 + \max\left(\frac{v_{\text{high}} - \text{avg speed}}{1}, 0\right)^2 \right]$$
- Helps avoid driving too slow or too fast.
- Good for aligning with speed limits or passenger preferences.


2. **Comfort**: Penalizes excessive jerk (acceleration change), which causes discomfort.

$$E_{\text{comfort}} = \mathbb{E}\left[ \max\left( j_{\max} - \left| \frac{d^3 x}{d\tau^3} \right|, 0 \right)^2 \right]$$
	•	Lower jerk → smoother ride
	•	Can be extended to lateral jerk, acceleration, etc.


3. **Collision Avoidance**: Penalizes proximity to other vehicles using signed distance.

$$E_{\text{collision}} = \sum_{m, \tau} \Psi\left(\omega \cdot \max\left(1 - \frac{D^\tau_m}{r}, 0\right)\right)$$
- $$D^\tau_m$$: distance between ego and neighbor m at time $$\tau$$
- $$\Psi(x) = e^x - x$$: smooth energy function
- High gradient only when near collision


4. **Staying within Drivable Area**: Penalizes deviation from the drivable lane area.

$$E_{\text{drivable}} = \sum_{\tau} \Psi\left(\omega_d \cdot \text{SignedDistanceFromLane}(x^\tau_{\text{ego}})\right)$$
- Encourages the vehicle to stay inside legal lanes
- Works well with map-based signed distance fields (SDF)


Combination

We can linearly combine multiple energies at inference time:

$$E_{\text{total}} = \lambda_1 E_{\text{collision}} + \lambda_2 E_{\text{comfort}} + \lambda_3 E_{\text{speed}} + \cdots$$
- All terms must be differentiable w.r.t. the trajectory
- No retraining is needed

#### Implementation

Make the model:
- Robust to perturbations and distribution shifts
- Efficient at inference time
- Compatible with control systems

Key Components

1. Data Augmentation (for Robustness)

They add random perturbations to the current ego state during training with small random changes in:
- Position (x, y)
- Heading (\theta)
- Speed, acceleration

➡ This simulates out-of-distribution (OOD) conditions and trains the model to recover toward the correct trajectory.

Then they apply interpolation to generate a physically feasible trajectory from the perturbed start to the original future path.


2. Ego-Centric Transformation

Before feeding into the model:
- All coordinates are transformed into ego vehicle’s local frame
- This reduces variation and simplifies learning


3. Normalization
- Apply z-score normalization to trajectory coordinates, especially longitudinal direction
- Reason: ego’s longitudinal movement is much larger than lateral → imbalance hurts training


4. Efficient Inference
- Use DPM-Solver for fast sampling (denoising)
- Use low-temperature sampling to reduce randomness and improve trajectory determinism

➡ They achieve:
- 20 Hz inference speed
- Plan for 8 seconds at 10 Hz (i.e., 80 trajectory points)


### Experiments

### Notes
