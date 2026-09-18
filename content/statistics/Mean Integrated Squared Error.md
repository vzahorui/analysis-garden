---
tags:
  - statistics
aliases:
  - MISE
---
Mean Integrated Squared Error (MISE) is a metric used to measure the global performance and accuracy of a non-parametric function estimator, most commonly a [[Kernel Density Estimation|Kernel Density Estimator]] (KDE). It is also used for selecting a bin size for [[Histogram]].

# Formula

Given an unknown true [[Probability Density Function]] $f(x)$ and an estimate $\hat{f}(x)$, MISE measures the expected total squared distance between the two curves:

$$\text{MISE}(\hat{f}) = \mathbb{E} \left[ \int \big(\hat{f}(x) - f(x)\big)^2 dx \right]$$
# Why not just MSE?

When estimating a single fixed value $\theta$ with $\hat{\theta}$, we evaluate accuracy using standard [[Mean Squared Error]] (MSE)**:

$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[(\hat{\theta} - \theta)^2\right] = \text{Var}(\hat{\theta}) + \big(\text{Bias}(\hat{\theta})\big)^2$$

However, a probability density function $f(x)$ is a continuous curve across a continuum of points, not a single scalar:

- **Pointwise MSE**—$\text{MSE}\big(\hat{f}(x)\big)$—only tells you how well your model performs at a single specific location $x$.
- **MISE** aggregates point-by-point errors across the entire domain into a single scalar summary value.
