---
tags:
  - ML/deep-learning
  - ML/activation-function
---
**Mish** is a self-regularized, non-monotonic neural network activation function. It gained widespread adoption in [[Deep Learning Concepts|Deep Learning]] architectures (most notably YOLOv4) due to its performance improvements over traditional activations like [[ReLU]] and [[SiLU|Swish]].

## Mathematical Definition

Mish maps an input $x$ using a combination of the hyperbolic tangent ($\tanh$) and the [[Softplus function]]:

$$f(x) = x \cdot \tanh(\text{softplus}(x)) = x \cdot \tanh(\ln(1 + e^x))$$

![[Mish-1791047037938.webp]]

## How Mish Compares to GELU & SiLU

In many ways it is similar to [[GELU]] and [[SiLU]].
### Visual Shape & Negative Dip

Mish, SiLU, and GELU share almost identical trajectories for positive numbers ($x > 0$). Their differences lie primarily in the depth of their negative dips:

- **GELU** has the shallowest dip ($\approx -0.170$).
- **SiLU** has a deeper dip ($\approx -0.278$).
- **Mish** has the deepest negative dip ($\approx -0.310$).

The slightly deeper bump in Mish allows marginally more negative information flow before fully suppressing negative inputs.
### Computational Trade-off

The primary downside of Mish is its computational complexity. Calculating $e^x$, $\ln(\cdot)$, and $\tanh(\cdot)$ in sequence requires multiple transcendental operations per neuron pass.

- While modern PyTorch/CUDA implementations use custom CUDA kernels or fast-math approximations to mitigate this overhead, **SiLU remains computationally cheaper** in hardware accelerator pipelines.

### Where Each Functions Best

- [[Transformer]]s & [[LLM]]s: Prefer [[GELU]] and [[SiLU]]/[[Gated Linear Units#SwiGLU The Modern LLM Standard|SwiGLU]] due to their efficient hardware implementation and established performance at massive parameter scale.
- [[Computer Vision Concepts|Computer Vision]] & [[Convolutional Neural Network|CNN]]s: **Mish** frequently outperforms [[ReLU]] and [[SiLU|Swish]] in deep convolutional networks (such as YOLOv4 backbones and [[ResNet]]) where smooth gradients across many residual layers improve generalization accuracy.