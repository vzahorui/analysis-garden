---
tags:
  - ML/activation-function
  - ML/deep-learning
aliases:
  - GLU
  - gated unit
---
In a standard feed-forward layer with input $x$, linear transformations $W$ and $V$, and biases $b$ and $c$, a classic GLU is defined via [[Gating]] as:

$$\text{GLU}(x, W, V, b, c) = (xW + b) \odot \sigma(xV + c)$$

- **Linear Branch:** $(xW + b)$ provides unconstrained linear features.
- **[[Sigmoid Function|sigmoid]] Branch:** $\sigma(xV + c)$ produces values in $(0, 1)$ to dynamically scale the linear features.

### Why Gating Works So Well

1. **[[Saturation and Vanishing Gradient|Vanishing Gradient]] Protection**: The linear path $(xW + b)$ allows linear gradients to propagate backward without passing through non-linear activations, dramatically easing gradient flow in deep architectures.
2. **Dynamic Feature Selection:** The network can learn to conditionally zero out irrelevant signals based on the input context.

## SwiGLU: The Modern [[LLM]] Standard

**SwiGLU** ([[SiLU|Swish]] Gated Linear Unit) replaces the Sigmoid function in the gate component with the **[[SiLU|Swish]]/[[SiLU]]** activation ($\text{Swish}_1(x) = x \cdot \sigma(x)$).

### Mathematical Formula

$$\text{SwiGLU}(x, W, V) = \text{Swish}(xW) \odot xV$$

_(Note: Biases are typically omitted in modern [[Transformer]] implementations like LLaMA)._

## Architectural Difference: Standard FFN vs SwiGLU FFN

In a traditional Transformer Feed-Forward Network (FFN), input $x$ undergoes two linear projections:

$$\text{FFN}_{\text{Standard}}(x) = \text{GELU}(x W_1) W_2$$

In a **SwiGLU FFN**, input $x$ undergoes **three** linear projections ($W$, $V$, and $W_2$):

$$\text{FFN}_{\text{SwiGLU}}(x) = \left( \text{Swish}(x W) \odot x V \right) W_2$$

To keep parameter counts and floating-point operations (FLOPs) equal when upgrading a model from a standard FFN to SwiGLU, the hidden dimension $d_{\text{ff}}$ is typically reduced to roughly $\frac{2}{3}$ of its original size.

## Why SwiGLU is Dominant in LLMs

1. **Double Non-Linearity:** SwiGLU combines two smooth curves (Swish and element-wise multiplication), giving the network a more expressive capacity per layer.
2. **Superior Optimization:** Empirical studies across large-scale language modeling show that SwiGLU consistently achieves lower perplexity and better downstream benchmark scores than [[GELU]] or standard [[ReLU]] FFNs at equivalent compute budgets.