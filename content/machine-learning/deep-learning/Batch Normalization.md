---
tags:
  - ML/deep-learning
---
**Batch Normalization (BatchNorm)** is a technique used in deep [[Neural Network|Neural Networks]] to make training faster, more stable, and less sensitive to parameter initialization.

## The Core Problem: Internal Covariate Shift

As a deep network trains, the weights of early layers update. Consequently, the distribution of inputs to deeper layers constantly shifts throughout training. Deep layers must continuously adapt to these changing input distributions, which slows down convergence and requires very low learning rates and cautious weight initialization.

### How Batch Normalization Works

For a given mini-batch of [[Activation Functions|activations]] $\mathcal{B} = \{x_1, x_2, \dots, x_m\}$ at a specific layer:

1. **Calculate Mini-Batch Mean:**

$$\mu_{\mathcal{B}} = \frac{1}{m} \sum_{i=1}^{m} x_i$$

2. **Calculate Mini-Batch Variance:**

$$\sigma_{\mathcal{B}}^2 = \frac{1}{m} \sum_{i=1}^{m} (x_i - \mu_{\mathcal{B}})^2$$
3. **Normalize Activations:**

Scale activations to have zero mean and unit variance ($\epsilon$ is a small constant for numerical stability):

$$\hat{x}_i = \frac{x_i - \mu_{\mathcal{B}}}{\sqrt{\sigma_{\mathcal{B}}^2 + \epsilon}}$$

4. **Scale and Shift (Learnable Parameters):**

Allow the network to preserve representational power by learning optimal scale ($\gamma$) and shift ($\beta$) parameters:

$$y_i = \gamma \hat{x}_i + \beta$$

_If $\gamma = \sqrt{\sigma_{\mathcal{B}}^2 + \epsilon}$ and $\beta = \mu_{\mathcal{B}}$, the transform restores the original inputs._

### Key Benefits

- **Faster Training:** Allows significantly higher learning rates without the risk of [[Exploding and Vanishing Gradients]].
- **Less Sensitivity to Initialization:** Reduces reliance on precise weight initialization schemes (like [[Xavier Initialization|Xavier]] or [[He Initialization|He]] initialization).
- **Slight [[Regularization]] Effect:** Mini-batch noise acts as a mild regularizer, often reducing the need for high [[Dropout]] rates.
- **Smoother Loss Landscape:** Smooths the optimization landscape, enabling [[gradient descent]] to take more predictable steps.

### When to Use (and When Not To)

- **Where it excels:** [[Convolutional Neural Network]]s (CNNs) and deep Feedforward Networks (MLPs).

- **Where to be careful:**
    - **Small Batch Sizes:** If the mini-batch size is too small (e.g., 2–4), batch mean and variance become noisy and unreliable.
    - **[[Recurrent Neural Networks]] (RNNs):** BatchNorm struggles across variable sequence lengths (Layer Normalization is preferred here).