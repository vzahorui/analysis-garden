---
tags:
  - ML/deep-learning
aliases:
  - He
---
**He** initialization (also known as **Kaiming initialization**) is a weight initialization method designed specifically for deep [[Neural Network|Neural Networks]] that use **non-linear activation functions with zero-rectification**, primarily [[ReLU]] (Rectified Linear Unit) and its variants like **LeakyReLU** and **PReLU**.

It resolved the training instability and vanishing signal issues that occurred when training deep networks with ReLU using older methods like [[Xavier Initialization|Xavier]]/Glorot initialization.

### The Underlying Problem It Solves

When initializing weights in a neural network, the main goal is to prevent the variance of activation signals from exploding or shrinking as signals flow forward through layers, and to prevent [[Exploding and Vanishing Gradients]] and [[Saturation and Vanishing Gradient|Vanishing Gradients]] during [[Backpropagation]].

#### Why Xavier Fails with ReLU

Xavier initialization sets the weight variance to $\text{Var}(w) = \frac{1}{n_{\text{in}}}$. It assumes the activation function is linear around zero with a derivative near $1$ (like [[Hyperbolic Tangent|tanh]] and [[Sigmoid Function|sigmoid]]).

However, ReLU sets all negative values to zero ($f(x) = \max(0, x)$). Assuming a symmetric distribution around zero for input activations:

- Roughly **50% of the inputs to a ReLU layer are zeroed out**.
- This cuts the variance of the output in half:

$$\text{Var}(\text{ReLU}(y)) = \frac{1}{2} \text{Var}(y)$$

If you initialize weights using Xavier variance, the variance of activations drops by a factor of $\frac{1}{2}$ at every layer:

$$\text{Var}(\text{Layer}_L) \approx \left(\frac{1}{2}\right)^L \text{Var}(\text{Input})$$

In a network with 20 layers, the signal variance drops to $\left(\frac{1}{2}\right)^{20} \approx 0.000001$ of its initial value, causing activations and backpropagated gradients to vanish completely.

### Mathematical Intuition & Derivation

For a single layer without bias, the linear combination is:

$$y = \sum_{i=1}^{n_{\text{in}}} w_i x_i$$

Assuming zero-mean inputs $x_i$ and weights $w_i$ drawn independently:

$$\text{Var}(y) = n_{\text{in}} \cdot \text{Var}(w) \cdot \text{Var}(x)$$

When passing $y$ through ReLU, since half the distribution is zeroed out, the variance of the activated output $a = \text{ReLU}(y)$ becomes:

$$\text{Var}(a) = \frac{1}{2} \text{Var}(y) = \frac{1}{2} \cdot n_{\text{in}} \cdot \text{Var}(w) \cdot \text{Var}(x)$$

To preserve signal scale across layers, we want $\text{Var}(a) = \text{Var}(x)$. Setting $\frac{1}{2} \cdot n_{\text{in}} \cdot \text{Var}(w) = 1$ yields:

$$\text{Var}(w) = \frac{2}{n_{\text{in}}}$$

By doubling the weight variance compared to Xavier ($\frac{2}{n_{\text{in}}}$ vs $\frac{1}{n_{\text{in}}}$), He initialization perfectly offsets the variance drop caused by ReLU's zero-rectification.

### Formulas

Depending on whether weights are drawn from a [[Normal Distribution|Normal]] or Uniform distribution:

#### 1. He Normal Initialization

Weights are sampled from a zero-mean normal distribution:

$$w \sim \mathcal{N}\left(0, \sigma^2\right) \quad \text{where} \quad \sigma = \sqrt{\frac{2}{n_{\text{in}}}}$$

#### 2. He Uniform Initialization

Weights are sampled uniformly from $[-a, a]$:

$$w \sim U\left[-\sqrt{\frac{6}{n_{\text{in}}}}, \sqrt{\frac{6}{n_{\text{in}}}}\right]$$

_(Since the variance of $U[-a, a]$ is $\frac{a^2}{3}$, setting $\frac{a^2}{3} = \frac{2}{n_{\text{in}}}$ gives $a = \sqrt{\frac{6}{n_{\text{in}}}}$)._

### Adaptation for LeakyReLU

For **LeakyReLU** ($f(x) = \max(\alpha x, x)$ where $\alpha < 1$ is the negative slope), negative inputs are scaled by $\alpha$ rather than zeroed out. The variance formula adapts to:

$$\text{Var}(w) = \frac{2}{1 + \alpha^2} \cdot \frac{1}{n_{\text{in}}}$$

- When $\alpha = 0$ (standard ReLU), this reduces to $\frac{2}{n_{\text{in}}}$.
- When $\alpha = 1$ (linear activation), this reduces to $\frac{1}{n_{\text{in}}}$ (Xavier variance).
