---
tags:
  - ML
---
The **Softplus** function is a smooth, [[Derivative|differentiable]] approximation of the [[ReLU]] (Rectified Linear Unit) [[Activation Functions|activation]] function.

While ReLU abruptly bends at zero ($f(x) = \max(0, x)$), Softplus creates a smooth curve, avoiding the sharp "elbow" at the origin.
## Mathematical Definition

$$\text{Softplus}(x) = \ln(1 + e^x)$$

### Key Properties

- **Output Range:** $(0, \infty)$ — It produces strictly positive outputs.
- **Derivative:** The derivative of Softplus is the Logistic [[Sigmoid Function]]:
$$\frac{d}{dx}\text{Softplus}(x) = \frac{e^x}{1 + e^x} = \sigma(x)$$

![[Softplus-1791039831973.webp]]

## Common Use Cases

1. **Ensuring Positive Values:** Since its output is always strictly greater than zero, Softplus is frequently used in [[Machine Learning Concepts|machine learning]] models to parametrise positive quantities, such as the **variance ($\sigma^2$)** or **scale parameter** in [[Variational Autoencoder]]s (VAEs) and [[Bayesian neural network]]s.
2. **Smooth Approximations:** Used in optimization problems or continuous-time physics/differential models where everywhere-differentiable activation functions are mathematically required.

### Numerical Stability Note

When implementing Softplus in code, computing $\ln(1 + e^x)$ directly can cause **numerical overflow** for large positive values of $x$ (e.g., $e^{100}$ exceeds floating-point limits).

In practice, frameworks like PyTorch or TensorFlow implement it with a stable conditional threshold:

$$\text{Softplus}(x) \approx \begin{cases} x & \text{if } x > \text{threshold (e.g., 20)} \\ \ln(1 + e^x) & \text{otherwise} \end{cases}$$