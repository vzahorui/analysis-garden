---
tags:
  - ML/activation-function
  - ML/deep-learning
aliases:
  - Swish
---
**SiLU** (Sigmoid Linear Unit) and **Swish** are essentially the same underlying [[Activation Functions|activation]] function family, with SiLU being the exact instance of Swish where the scale parameter $\beta = 1$.

Both functions take input $x$ and scale it by the output of a standard logistic sigmoid function $\sigma(x)$.

## Mathematical Definition

$$\text{Swish}_{\beta}(x) = x \cdot \sigma(\beta x) = \frac{x}{1 + e^{-\beta x}}$$

- **SiLU (Swish-1):** When $\beta = 1$, the expression simplifies to $\text{SiLU}(x) = x \cdot \sigma(x)$. This is the most widely implemented variant in modern [[Neural Network|Neural Networks]].
- **Parameterized Swish:** $\beta$ can either be a fixed hyperparameter or a learnable weight trained via [[backpropagation]].

![[SiLU-1791032716299.webp]]

### Impact of the Scale Parameter $\beta$

The parameter $\beta$ acts as an interpolation control between a pure linear function and a hard ReLU step function:

- **As $\beta \to 0$:** $\sigma(0 \cdot x) = 0.5$, so $\text{Swish}(x) \to \frac{x}{2}$ (a scaled linear function).
- **As $\beta \to 1$:** You get **SiLU** (standard Swish).
- **As $\beta \to \infty$:** $\sigma(\beta x)$ becomes an infinitely steep step function, causing Swish to converge directly into standard [[ReLU]] ($\max(0, x)$).

## Why Modern Architectures Favor SiLU/Swish

- **Self-Gated Architecture:** The function uses its own magnitude ($x$) to gate itself via $\sigma(x)$. Large positive inputs pass cleanly through, while negative inputs are smoothly suppressed according to their magnitude.
- **Gradient Flow in Deep Nets:** The small negative dip allows subtle gradient signals to propagate backward even through inactive neurons, preventing "dead" unit problems common in standard ReLU networks.
- **Empirical Dominance in Large Models:** SiLU is currently the default activation choice in state-of-the-art open [[LLM]] backbones (such as Meta's LLaMA series using SwiGLU variant blocks) and computer vision models like EfficientNet and YOLO.
- Less computationally intensive than [[GELU]].


