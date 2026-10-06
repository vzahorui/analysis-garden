---
tags:
  - ML/deep-learning
aliases:
  - saturation
  - vanishing gradient
---
## Saturation

**Saturation** refers to a [[Neural Network|neuron]]'s [[Activation Functions|activation]] state when its input (the weighted sum $z = w^Tx + b$) moves into extreme positive or negative regions.

For the standard [[Sigmoid function]]:

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

- **Saturated High:** When $z \gg 0$, $\sigma(z) \approx 1$.
- **Saturated Low:** When $z \ll 0$, $\sigma(z) \approx 0$.

In these saturated flat regions, big changes in the input $z$ yield virtually zero change in the output $\sigma(z)$.

## Vanishing Gradient

The **vanishing gradient** is a optimization issue during training where the weight updates during [[backpropagation]] become extremely small, or vanish to zero, preventing earlier layers in the network from learning.

By the [[Derivative#Fundamental Rules|chain rule]], the gradient of the loss $\mathcal{L}$ with respect to a weight $w_i$ in a layer is multiplied by the derivative of the activation function, $\sigma'(z)$:

$$\frac{\partial \mathcal{L}}{\partial w_i} = \frac{\partial \mathcal{L}}{\partial a} \cdot \sigma'(z) \cdot x_i$$

The [[derivative]] of the [[Sigmoid function]] is given by:

$$\sigma'(z) = \sigma(z)(1 - \sigma(z))$$

- The maximum possible value of $\sigma'(z)$ is **$0.25$** (at $z = 0$).
- When $z$ moves into a **saturated region** ($\sigma(z) \approx 1$ or $\sigma(z) \approx 0$), the derivative approaches **zero**:

$$\lim_{z \to \pm\infty} \sigma'(z) = 0$$

When gradients are multiplied across many layers during backpropagation, multiplying by values near $0$ causes the overall gradient to rapidly decay to near-zero as it moves backward toward the input layer.