---
tags:
  - ML/deep-learning
---
Network initialization is the process of setting the initial weights and biases of a [[Neural Network]] before training begins.

Proper initialization ensures that signal strength (variance of activations and gradients) remains stable as information flows forward through layers and gradients flow backward during [[backpropagation]].

### Why Initialization Matters

If weights are initialized poorly, neural networks fail to learn due to two primary mathematical failure modes:

- [[Exploding Gradients]]: If weights are initialized too large, activations and gradients grow exponentially layer by layer, leading to numerical overflow (`NaN` values) or unstable updates.
- **Vanishing Gradients:** If weights are initialized too small, activation values and gradients exponentially shrink toward zero as they pass through layers. Deep layers stop updating, and the network fails to train. In principle, this is the same problem as [[Exploding Gradients]].
- **Symmetry Breaking:** Setting all weights to a constant value (such as all zeros) forces every neuron in a layer to compute the exact same output and receive the exact same gradient update. The neurons remain identical throughout training, reducing the layer's capacity to that of a single neuron.

Good initialization breaks symmetry and keeps signal variance stable across layers, allowing gradients to flow effectively so the network can actually learn.

## Variance-preserving idea

Suppose a layer has $n_{in}$​ inputs and weights with variance $\sigma_w^2$​. If inputs have variance $\sigma_x^2$​, then roughly:

$$Var(y)≈n_{in} \sigma_w^2 Var(x)$$

To keep the output variance equal to the input variance, we want:

$$\sigma_w^2=\frac{1}{n_{in}}​$$

This is the basic intuition behind most modern initialization schemes.

## Common initialization methods

* [[Xavier Initialization]] for [[Hyperbolic Tangent|tanh]] and [[Sigmoid Function|sigmoid]] activations.
* [[He Initialization]] for [[ReLU]] and its variants.

## Bias Initialization

Biases could be kept at zero unless you have a specific reason not to do so.