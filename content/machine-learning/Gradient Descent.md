---
tags:
  - ML
---
Gradient Descent is an optimization algorithm used to minimize a [[Loss vs Metric|loss]] function by iteratively updating model parameters (weights and biases) in the direction of steepest decrease.

## Core Intuition

Imagine standing near the top of a fog-covered mountain. Your goal is to reach the lowest point of the valley, but you cannot see the path ahead.

To find your way down:

1. You feel the slope of the ground beneath your feet.
2. You identify which direction tilts downward most steeply.
3. You take a step in that direction.
4. You repeat this process until the ground flattens out.

In machine learning, the mountain represents the **loss function** $L(\theta)$, the altitude is the current **[[Residual vs Error|error]] rate**, and your location represents the current values of your **parameters** $\theta$.

## Mathematical Framework

The **[[Derivative#Gradient]]** $\nabla_\theta L(\theta)$ is a vector of partial derivatives pointing in the direction of the greatest rate of increase of the loss function. To decrease the loss, parameters are moved in the **opposite** direction of the gradient.

The update rule at iteration $t$ is defined as:
$$\theta_{t+1} = \theta_t - \alpha \nabla_\theta L(\theta_t)$$

where:

- $\theta_t$ is the parameter vector at step $t$.
- $\alpha$ is the **learning rate** (hyperparameter controlling step size).
- $\nabla_\theta L(\theta_t)$ is the gradient vector evaluated at $\theta_t$.

![[gradient_descent.gif]]

## 3. Key Dynamics: Learning Rate ($\alpha$)

The hyperparameter $\alpha$ determines the step magnitude along the negative gradient vector:

|**Learning Rate**|**Effect on Optimization**|**Risk**|
|---|---|---|
|**Too Large**|Overshoots the local minimum|Divergence or oscillation around the minimum|
|**Too Small**|Very small step sizes|Slow convergence; risks getting stuck in local minima or saddle points|
|**Optimal**|Smooth decrease toward the minimum|Efficient convergence in reasonable time|
## Main Variants

* **Batch Gradient Descent**: Computes gradient over the entire dataset per step. Deterministic and smooth trajectory, but computationally expensive and slow for large datasets.
* **Stochastic Gradient Descent (SGD)**: Computes gradient using 1 random sample per step. Fast updates and lower memory footprint, but introduces high variance in update trajectories. Additinally it has hight I/O overhead.
* **Mini-Batch Gradient Descent**:  Computes gradient over a small batch (e.g., 32, 64, 128, usually a multiple of power of 2) per step. Maximizes computational efficiency via vectorized tensor operations on modern modern hardware (GPUs/TPUs).
