---
tags:
  - statistics
aliases:
  - Kernel Density Estimator
  - KDE
---
**Kernel Density Estimation (KDE)** is a non-parametric way to estimate the probability density function (PDF) of a continuous random variable.

## The Intuition: How KDE Works

1. **Place a "bump" over every data point:** Imagine taking each observed data point and placing a symmetric probability curve (called the **kernel**) centered directly on top of it.
2. **Choose the width of the bump:** The spread of this bump is controlled by a parameter called the **bandwidth** ($h$).
3. **Sum all the bumps together:** At any point along the x-axis, add up the heights of all the individual kernels.
4. **Normalize:** Divide the total sum by the number of data points $n$ so that the total area under the final curve equals $1$.

## Mathematical Definition

For a sample of independent data points $x_1, x_2, \dots, x_n$ drawn from an unknown distribution, the univariate kernel density estimator is defined as:

$$\hat{f}_h(x) = \frac{1}{n h} \sum_{i=1}^{n} K\left( \frac{x - x_i}{h} \right)$$

Where:
- $x$ is the evaluation point where you want to calculate the density. $x_1$ is the reference point (center of the kernel).
- $h > 0$ is the **bandwidth**, acting as a smoothing parameter. Higher bandwidth -> more smooting.
- $K(\cdot)$ is the **kernel function**, a symmetric probability density function satisfying $\int_{-\infty}^{\infty} K(u) \, du = 1$.
- $n$ is the total number of data points. Dividing by $n$ is what achieves normalization here,

### Key Components

#### 1. Choice of Kernel ($K$)

The kernel function dictates the shape of the individual bumps placed over each point. Common choices include:

- **[[Normal Distribution|Gaussian]] (Normal):** $K(u) = \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2}u^2}$ _(most common due to smooth differentiability)_
- **Epanechnikov:** $K(u) = \frac{3}{4}(1 - u^2)$ for $\vert{}u\vert{} \le 1$ _(statistically optimal in minimizing mean square error)_
- **Uniform (Boxcar):** $K(u) = \frac{1}{2}$ for $\vert{}u\vert{} \le 1$
- **Triangular:** $K(u) = (1 - \vert{}u\vert{})$ for $\vert{}u\vert{} \le 1$

![[Kernel Density Estimation-1789918471862.webp]]

> **Note:** The choice of kernel shape has a relatively minor effect on the overall density estimate compared to the choice of bandwidth.

#### 2. Choice of Bandwidth ($h$)

The bandwidth $h$ governs the trade-off between [[Bias and Variance]]:

- **Too Small ($h \to 0$):** Under-smoothed. The estimate exhibits high variance (overfitting) and appears jagged, reflecting random noise rather than the true underlying distribution.
- **Too Large ($h \to \infty$):** Over-smoothed. The estimate exhibits high bias (underfitting), obscuring genuine features like bimodal peaks or skewness.

**Common Bandwidth Selection Rules:**

- **Silverman's Rule of Thumb:** $h = 0.9 \cdot \min\left(\hat{\sigma}, \frac{IQR}{1.34}\right) \cdot n^{-1/5}$ (optimal when the true underlying data is roughly Gaussian).

![[Kernel Density Estimation-1789919476971.webp]]