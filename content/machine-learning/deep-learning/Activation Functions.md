---
tags:
  - ML/deep-learning
  - ML/activation-function
aliases:
  - activation function
  - activation
  - activations
---
This note is an overview of activation functions used in [[Neural Network|Neural Networks]].

# Classical Activations

* [[Sigmoid Function]] - used for an output layer in binary classification.
* [[Softmax Function]] - used for an output layer in multiclass classification. 

Sigmoid and Softmax inherently suffer from vanishing gradients in their mathematical formulation, but when paired with [[Cross-Entropy]] [[Loss vs Metric|loss]], this issue is mathematically eliminated at the output layer. 

Applying the chain rule to find the gradient of the loss with respect to the raw input logit $z_i$ simplifies to a linear expression:

$$\frac{\partial \mathcal{L}_{\text{CE}}}{\partial z_i} = \frac{\partial \mathcal{L}_{\text{CE}}}{\partial p_k} \cdot \frac{\partial p_k}{\partial z_i} = p_i - y_i$$
* [[Hyperbolic Tangent]]

# Piecewise Family

* [[ReLU]] note covers all of them.

# Smooth Self-Gated Activations

See [[Gating]]. While traditional gated architectures (like [[LSTM]]s or GRUs) use learnable parameters to compute gates, **self-gated activation functions** use the input $x$ itself (or a smooth transform of $x$) to act as its own gate.

* [[GELU]]
* [[SiLU]]
* [[Mish]]

# Gated Activations

* [[Gated Linear Units]] (including [[Gated Linear Units#SwiGLU The Modern LLM Standard|SwiGLU]])




