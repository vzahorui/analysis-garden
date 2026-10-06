---
tags:
  - ML/deep-learning
---
This is a concept originating from [[Regularization#L2 Regularization (Ridge)]].

**Weight decay and $L_2$ regularization are mathematically distinct**, even though they produce identical parameter updates in plain Stochastic [[Gradient Descent]] (SGD).

Symbols used here match [[Adaptive Optimizers]]: parameters $\theta_t$, learning rate $\eta$, decay/L2 strength $\lambda$, data-loss gradient $g_t=\nabla_\theta\mathcal{L}(\theta_t)$.

## The Core Difference

- **$L_2$ Regularization** modifies the **loss** by adding a penalty:

$$\mathcal{L}_{\text{new}}(\theta) = \mathcal{L}(\theta) + \frac{\lambda}{2} \Vert\theta\Vert^2$$

- **Weight Decay** modifies the **update** by shrinking parameters each step:

$$\theta_{t+1} = (1 - \eta\lambda) \theta_t - \eta g_t$$

## Why They Equate in Standard SGD

In SGD without adaptive scaling or momentum, the gradient of the $L_2$-regularized loss is:

$$\nabla \mathcal{L}_{\text{new}}(\theta_t) = g_t + \lambda \theta_t$$

Plugging into the SGD step:

$$\theta_{t+1} = \theta_t - \eta (g_t + \lambda \theta_t) = (1 - \eta\lambda) \theta_t - \eta g_t$$

Same update as decoupled weight decay with the same $\lambda$. The equivalence uses one hyperparameter $\lambda$ and the factor $\eta\lambda$.

## Where They Diverge

The equivalence breaks in two main scenarios.

### Scenario A: [[Adaptive Optimizers]] (Adam, RMSProp)

Write the Adam adaptive scale as $s_t = \sqrt{\hat{v}_t} + \epsilon$. Moments $\hat{m}_t$, $\hat{v}_t$ are defined in [[Adaptive Optimizers]].

- **$L_2$ inside Adam (coupled):** the penalty rides with the gradient through the adaptive scale:

$$\theta_{t+1} = \theta_t - \frac{\eta}{s_t} (g_t + \lambda \theta_t)$$

(Full Adam would build $\hat{m}_t$ from the regularized gradient $g_t+\lambda\theta_t$; the teaching point is the same: $\lambda\theta_t$ is divided by $s_t$.)

Weights with large historical gradients get **weaker** effective decay; weights with small historical gradients get **stronger** decay.

- **Decoupled Weight Decay (AdamW):** moments use only the unregularized $g_t$; decay sits outside $s_t$:

$$\theta_{t+1} = (1 - \eta\lambda) \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$

Uniform relative shrinkage across parameters, independent of the adaptive denominator.

#### Which Is Better

A large gradient lets a weight move quickly. Movement is not the same as regularization.

Weight decay should act like gravity: a predictable pull toward zero proportional to parameter size ($-\lambda\theta$).

When $L_2$ is folded into Adam, that pull is warped by $s_t$. **AdamW** restores uniform decay.

### Scenario B: SGD with Momentum

With momentum, putting $L_2$ in the loss feeds $\lambda\theta$ into the velocity accumulator. True weight decay shrinks $\theta_t$ directly (factor $1-\eta\lambda$) instead of mixing the penalty into past velocities.

## Key Benefits of Using AdamW

- **Better Generalization:** AdamW usually beats Adam+$L_2$ on test error.
- **Predictable Tuning:** $\lambda$ is the weight-decay strength next to $\eta$; you are not silently retuning effective L2 every time you change the learning rate inside an adaptive denominator.
- **Industry Standard:** Transformers, LLMs, and Vision Transformers typically default to **AdamW**.

## Considerations When Using in [[Neural Network|Neural Networks]]

> [!warning]
> Weight decay is applied **only to weights ($\mathbf{W}$)**, not to biases ($\mathbf{b}$). Regularizing biases can cause underfitting by restricting the model's ability to shift activation thresholds.
