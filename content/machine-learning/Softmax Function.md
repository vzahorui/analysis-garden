---
tags:
  - ML/classification
  - ML/deep-learning
---
The softmax function converts a vector of raw, unnormalized real numbers (called **logits**) into a valid [[Probability Distributions|Probability Distribution]]. 

This is similar to what [[Sigmoid Function]] does to logits in the context of [[Logistic Regression]].

It is most commonly used as the final activation layer in multi-class [[Classification]] [[Neural Network|Neural Networks]] (and in attention mechanisms, like Transformers) to make raw model predictions interpretable as percentages or probabilities.

## The Mathematical Formula

For a vector of raw scores $z = [z_1, z_2, \dots, z_K]$ with $K$ classes, the softmax probability $S(z)_i$ for class $i$ is calculated as:

$$S(z)_i = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}}$$

### How it breaks down:

1. **Exponentiation ($e^{z_i}$):** Computes $e$ raised to the power of each raw score. This does two critical things:
    - **Ensures positivity:** $e^x$ is always greater than $0$, eliminating negative values.
    - **Amplifies differences:** Larger values become exponentially larger, making the model's top choices stand out more clearly.
2. **Normalization ($\sum e^{z_j}$):** Divides each exponentiated value by the sum of all exponentiated values. This forces the resulting outputs to **sum to 1.0 (100%)**.

## Step-by-Step Example

Imagine a model trying to classify an image into 3 categories: **Cat**, **Dog**, or **Bird**.

1. **Raw Logits ($z$):**
    $\text{Cat} = 2.0, \quad \text{Dog} = 1.0, \quad \text{Bird} = 0.0$
2. **Exponentiate ($e^z$):**
    - $e^{2.0} \approx 7.389$
    - $e^{1.0} \approx 2.718$
    - $e^{0.0} = 1.000$
3. **Sum of Exponentials:**
    $\text{Sum} = 7.389 + 2.718 + 1.000 = 11.107$
4. **Normalize to Probabilities:**
    - $P(\text{Cat}) = \frac{7.389}{11.107} \approx \mathbf{0.665 \text{ (66.5\%)}}$
    - $P(\text{Dog}) = \frac{2.718}{11.107} \approx \mathbf{0.245 \text{ (24.5\%)}}$
    - $P(\text{Bird}) = \frac{1.000}{11.107} \approx \mathbf{0.090 \text{ (9.0\%)}}$

Notice that $0.665 + 0.245 + 0.090 = 1.00$.

## Key Properties & Behavior

- **Output Range:** Every output value lies strictly between $0$ and $1$.
- **Preserves Order:** The relative ranking of logits remains unchanged (if $z_1 > z_2$, then $S(z)_1 > S(z)_2$).
- **Multi-Class Mutual Exclusivity:** Because all outputs sum to 1, an increase in the probability of one class forces a decrease in the combined probabilities of the other classes.
- **Temperature Scaling:** Softmax is often modified with a temperature parameter $T$: $S(z)_i = \frac{e^{z_i / T}}{\sum e^{z_j / T}}$. High temperature softens the output distribution (making probabilities more equal), while low temperature makes it sharper (closer to an `argmax`).

## Practical Implementation Note (Numerical Stability)

In software (like PyTorch, TensorFlow, or NumPy), computing $e^{z_i}$ directly for large numbers (e.g., $z_i = 1000$) causes **numerical overflow** ($e^{1000} \to \infty$).

To fix this, implementations subtract the maximum value $\max(z)$ from all elements before exponentiating:

$$S(z)_i = \frac{e^{z_i - \max(z)}}{\sum_{j=1}^{K} e^{z_j - \max(z)}}$$

Mathematically, this produces the exact same probability output but keeps the largest exponent at $e^0 = 1$, preventing float overflow.