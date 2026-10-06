---
tags:
  - ML/deep-learning
aliases:
  - Xavier
---
**Xavier initialization** (also known as **Glorot initialization**) is a weight initialization technique designed to keep the variance of activations and [[Derivative|gradients]] roughly constant across all layers of a deep [[Neural Network]] during forward and backward passes.

It solves the signal exploding/vanishing problem in networks with symmetric activation functions centered near zero (such as [[Hyperbolic Tangent|tanh]] and [[Sigmoid Function|sigmoid]]).

### The Problem It Solves

If weights are initialized too large or too small:

- **Weights too large:** The variance of activations grows exponentially with network depth, pushing activations into the saturated regions of activation functions (where slopes are nearly zero) and causing [[exploding gradients]] or [[Saturation and Vanishing Gradient|vanishing gradients]].
- **Weights too small:** Activations shrink toward zero layer by layer, leading to **vanishing signals** where deeper layers receive almost no meaningful gradient updates.

### Mathematical Derivation

For a linear layer output $y = \sum_{i=1}^{n_{\text{in}}} w_i x_i$ (assuming zero-mean inputs and weights, and independent variables), the variance of the output is:

$$\text{Var}(y) = n_{\text{in}} \cdot \text{Var}(w) \cdot \text{Var}(x)$$

To prevent activations from blowing up or collapsing, we want the variance of the output to match the variance of the input ($\text{Var}(y) = \text{Var}(x)$). This requires:

$$n_{\text{in}} \cdot \text{Var}(w) = 1 \implies \text{Var}(w) = \frac{1}{n_{\text{in}}}$$

Similarly, to keep the variance of backpropagated gradients stable from output to input, we need:

$$\text{Var}(w) = \frac{1}{n_{\text{out}}}$$

Taking the harmonic mean of both requirements gives the Xavier variance condition:

$$\text{Var}(w) = \frac{2}{n_{\text{in}} + n_{\text{out}}}$$

### Formulas

Depending on whether you draw weights from a [[Normal Distribution|Gaussian]] (Normal) or Uniform distribution:

#### 1. Normal Xavier Initialization

Weights are sampled from a zero-mean normal distribution:

$$w \sim \mathcal{N}\left(0, \sigma^2\right) \quad \text{where} \quad \sigma = \sqrt{\frac{2}{n_{\text{in}} + n_{\text{out}}}}$$

#### 2. Uniform Xavier Initialization

Weights are sampled uniformly from $[-a, a]$:

$$w \sim U\left[-\sqrt{\frac{6}{n_{\text{in}} + n_{\text{out}}}}, \sqrt{\frac{6}{n_{\text{in}} + n_{\text{out}}}}\right]$$

_(Note: For a uniform distribution $U[-a, a]$, variance is $\frac{a^2}{3}$. Setting $\frac{a^2}{3} = \frac{2}{n_{\text{in}} + n_{\text{out}}}$ yields $a = \sqrt{\frac{6}{n_{\text{in}} + n_{\text{out}}}}$)._