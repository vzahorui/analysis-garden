---
tags:
  - statistics
  - ML
aliases:
  - sigmoid
  - sigmoid activation
---
The **sigmoid function** (specifically the standard logistic function) is a mathematical function that takes any real-valued number and maps it into a value strictly between 0 and 1. It forms a characteristic "S"-shaped curve.

![[Sigmoid Function-1790513461083.webp]]

$$\sigma(x) = \frac{1}{1 + e^{-x}}$$
### Key Properties

- **Output Range:** Bounds all values between $(0, 1)$.
- **Symmetry:** Passes through $\sigma(0) = 0.5$.
- **Extremes:** As $x \to \infty$, $\sigma(x) \to 1$. As $x \to -\infty$, $\sigma(x) \to 0$.
- **Smooth Derivative:** The [[derivative]] can be expressed using the output itself:

$$\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))$$

### Key Applications

1. **Probability Output:** Because the output is strictly bounded between 0 and 1, [[Machine Learning Concepts|Machine Learning]] models (like logistic regression) treat $\sigma(x)$ as the probability of a binary [[Classification]] (e.g., $P(y = 1 \vert{} x)$).
2. **[[Neural Network]] Activation Function:** Historically used to simulate the firing rate of biological neurons (either inactive $\approx 0$ or fully active $\approx 1$).

### Drawback: Vanishing Gradient Problem

When $x$ becomes very large positive or very large negative, the curve becomes nearly flat (the derivative approaches 0). During backpropagation in deep neural networks, multiplying these tiny gradients causes training to slow down or stall completely. Modern architectures often favor [[ReLU]] (Rectified Linear Unit) for hidden layers, reserving Sigmoid primarily for the final output layer in binary classification tasks.