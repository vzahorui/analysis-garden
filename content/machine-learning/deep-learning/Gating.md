---
tags:
  - ML/deep-learning
---
In [[Neural Network|Neural Networks]], **gating** is a mechanism where one signal acts as a "valve" or "filter" to control how much information passes through from another signal.

Instead of passing an input through a single transformation, a gated system computes two separate pathways: a **value pathway** (the content) and a **gate pathway** (the valve), which are combined element-wise.

### What is a Gated [[Activation Functions|Activation]]?

In standard activation functions like [[ReLU]] or [[GELU]], a single function $f(x)$ takes an input and transforms it directly.

In a **gated activation**, the output is produced by multiplying two different functions element-wise ([[Hadamard Product]])

$$\text{Output} = f(x) \odot g(x)$$

- **$f(x)$ (Value Vector):** Generates the primary feature representation or content.
- **$g(x)$ (Gate Vector):** Evaluates to values strictly or smoothly between $0$ and $1$ (typically using a [[Sigmoid Function|sigmoid]] or another smooth activation). It determines _how much_ of $f(x)$ is allowed to pass through to the next layer.

If $g(x) \approx 1$, the feature passes completely. If $g(x) \approx 0$, the feature is suppressed.

## Self-Gating Activations

We can think of [[GELU]] and [[SiLU]] as self-gating activations because they do the gating implicitly. 