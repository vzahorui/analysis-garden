---
tags:
  - ML/deep-learning
  - ML/activation-function
---
The **GELU** (Gaussian Error Linear Unit) is an [[Activation Functions|activation]] function is widely used in modern transformer architectures, including BERT, GPT-2/3/4, RoBERTa, and ViT (Vision Transformers).

## Key Intuition: Probabilistic Dropout

Traditional activation functions apply a deterministic threshold to inputs:

- **[[ReLU]]** sets all negative inputs strictly to $0$ and keeps positive inputs as $x$.
- **GELU** scales the input $x$ by the probability that a [[Normal Distribution|Gaussian]] [[Set Theory#Random Variable|random variable]] is less than $x$.

Instead of deciding whether to keep or drop a neuron based purely on its sign, GELU scales an input depending on **how much greater it is than other inputs**. As $x$ decreases, the probability of dropping it increases. This makes GELU a smooth, probabilistic generalization of [[ReLU]] and [[Dropout]] combined.

## Mathematical Definition

Formally, GELU is defined as:

$$\text{GELU}(x) = x \cdot P(X \le x) = x \cdot \Phi(x)$$

where $\Phi(x)$ is the cumulative distribution function (CDF) of the standard Gaussian distribution $\mathcal{N}(0, 1)$.

## Behavior and Visual Comparison

- **For large positive $x$ ($x > 2$):** $\Phi(x) \approx 1$, so $\text{GELU}(x) \approx x$.
- **For large negative $x$ ($x < -2$):** $\Phi(x) \approx 0$, so $\text{GELU}(x) \approx 0$.
- **Near zero ($-2 \le x \le 2$):** GELU is smooth and non-monotonic. It dips slightly below zero (minimum value $\approx -0.17$ near $x \approx -0.75$) before rising back toward $0$.

![[GELU-1791031845314.webp]]

## Why [[Transformer]] Models Prefer GELU

1. **Smooth [[Derivative|gradients]]:** Unlike ReLU, which has a sharp discontinuity at $0$, GELU is smooth throughout. This prevents optimization instability during gradient descent in deep networks.
2. **Non-monotonicity:** The slight negative dip allows small negative inputs to convey information, helping deep transformer architectures retain gradient flow for subtle signals.
3. **Empirical Performance:** Models trained with GELU consistently outperform ReLU-based models on complex [[NLP Concepts|NLP]] and [[Computer Vision Concepts|Computer Vision]]] benchmarks.

## Limitations

Requires computing the Gaussian cumulative distribution function ($\Phi(x)$), which involves the error function ($\text{erf}$). Because $\text{erf}$ lacks a simple closed form, it requires heavy numerical approximations (or numerical integration) across **all** input values ($x > 0$ and $x < 0$).

### Approximate GELU

Because evaluating $\text{erf}$ directly is computationally expensive in deep neural networks (like Transformers), deep learning frameworks often use polynomial or hyperbolic tangent approximations:

$$\text{GELU}(x) \approx 0.5x \cdot \left(1 + \tanh\left(\sqrt{\frac{2}{\pi}} \left(x + 0.044715 x^3\right)\right)\right)$$

Even with this approximation, GELU requires multiplications, a cubic power ($x^3$), addition, and a transcendental hyperbolic tangent ($\tanh$) call for every single input, making it significantly heavier than ReLU and moderately heavier than [[ReLU#ELU (Exponential Linear Unit)]].