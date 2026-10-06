---
tags:
  - ML
aliases:
  - Adam
  - AdamW
---
Adaptive optimizers automatically adjust the learning rate for each parameter individually during training based on past [[Derivative|gradients]]. This addresses a core limitation of standard Stochastic [[Gradient Descent]] (SGD): using a single, fixed learning rate across all parameters often leads to slow convergence, oscillation in steep valleys, or getting stuck in saddle points.

## Gradient Descent with Momentum

Standard SGD stutters and oscillates when the loss surface curves much more steeply in one dimension than another (ravines/valleys). Momentum dampens these vertical oscillations and accelerates motion along the flat, consistent direction: like a heavy ball rolling down a hill.

Momentum maintains a velocity vector $u_t$ as an Exponential Moving Average (EMA) of past gradients:

$$u_t = \beta u_{t-1} + (1 - \beta) g_t$$

$$\theta_{t+1} = \theta_t - \eta u_t$$

_(where $\beta \in [0, 1)$, typically $0.9$)_

- **Pros:** Accelerates through flat regions and dampens high-frequency oscillations.
- **Cons:** Uses a uniform learning rate across all dimensions. If a parameter receives sparse or small gradients, progress remains slow.

## RMSProp (Root Mean Square Propagation)

While Momentum tracks the **direction** of gradients (1st moment), RMSProp tracks the **magnitude** of gradients (2nd moment). It scales the learning rate inversely proportional to the square root of recent gradient magnitudes.

RMSProp keeps an exponential moving average of squared gradients, $s_t$:

$$s_t = \beta s_{t-1} + (1 - \beta) g_t^2$$

$$\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{s_t + \epsilon}} \odot g_t$$

- **How It Works:**
    - If a parameter has historically large gradients ($s_t$ is large), its effective learning rate is reduced.
    - If a parameter has small or sparse gradients ($s_t$ is small), its effective learning rate is boosted.

- **Pros:** Effectively handles non-stationary objectives and ill-conditioned loss surfaces.
- **Cons:** Lacks the directional velocity benefits of momentum.

## Adam (Adaptive Moment Estimation)

Adam combines the core benefits of both Momentum and RMSProp. It tracks both the first moment $m_t$ (mean of gradients, like Momentum) and the second moment $v_t$ (uncentered variance of gradients, like RMSProp).

1. **Compute Moments:**

$$m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t \quad \text{(1st moment / Momentum)}$$

$$v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2 \quad \text{(2nd moment / RMSProp)}$$

2. **Bias Correction:**

Since $m_0$ and $v_0$ are initialized to zero, both estimates are heavily biased towards zero in early iterations. Adam corrects this via:

$$\hat{m}_t = \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t}$$

3. **Parameter Update:**

$$\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$

_(Typical hyperparameter values: $\beta_1 = 0.9$, $\beta_2 = 0.999$, $\epsilon = 10^{-8}$)_

- **Pros:** Industry standard default optimizer; highly robust, fast convergence, handles noisy and sparse gradients well.
- **Cons:** Can generalize worse than SGD with momentum on certain vision tasks; mishandles $L_2$ [[Weight Decay|weight decay]] regularization.

![[adaptive_optimizers.gif]]

## AdamW (Adam with Decoupled Weight Decay)

In standard SGD, $L_2$ [[Regularization|regularization]] ($\mathcal{L}_{\text{new}} = \mathcal{L} + \frac{\lambda}{2} \Vert\theta\Vert^2$) is mathematically equivalent to [[Weight Decay|weight decay]]:

$$\theta_{t+1} = (1 - \eta\lambda) \theta_t - \eta g_t$$

In Adam, $L_2$ passes through the adaptive denominator $\sqrt{\hat{v}_t}+\epsilon$, so parameters with large historical gradients receive **less** effective decay than parameters with small gradients. **AdamW** decouples weight decay from the adaptive gradient step.

AdamW builds $m_t$ and $v_t$ from the **unregularized** gradient $g_t$ only, then applies decay outside the adaptive scale:

$$\theta_{t+1} = (1 - \eta\lambda) \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$

- **Pros:** Restores true weight decay behavior and usually better generalization in [[Deep Learning Concepts|Deep Learning]] (standard in [[Transformer]] architectures like ViT and [[LLM]]s).

## Why First Moment = Direction, Second Moment = Magnitude

The terminology comes from probability theory and physics, where moments describe the shape of a set of values or a distribution:

### First Moment: $\mathbb{E}[g_t]$ (Mean/Direction)

The first moment tracks the **expected value** (running average) of the gradient vector itself:

$$m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t$$

Because $g_t$ contains signed values (positive or negative depending on which way the loss increases), averaging them preserves **net direction**:

* If the gradient points in the $+x$ direction 9 out of 10 times, the average $m_t$ remains strongly **positive**.
- If the gradient oscillates back and forth rapidly ($+1, -1, +1, -1$), the positive and negative signs **cancel out**, resulting in $m_t \approx 0$.

**Result**: The first moment acts as a low-pass filter that dampens random noise and retains the steady, underlying direction of steep descent.

### Second Moment: $\mathbb{E}[g_t^2]$ (Uncentered Variance/Magnitude)

The second moment tracks the exponential moving average of the **squared** gradients:

$$v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2$$

Squaring the gradient strips away the sign ($(-5)^2 = (+5)^2 = 25$).

- Because every term is non-negative, **no cancellation occurs**, regardless of whether the parameter is oscillating or moving smoothly.
- $v_t$ measures strictly **how large** the gradient steps have been on average along that coordinate axis—its overall variance or energy.

In RMSProp, dividing by $\sqrt{v_t + \epsilon}$ normalizes updates: parameters with massive gradients get scaled down, while parameters with tiny or sparse gradients get boosted.