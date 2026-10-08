---
tags:
  - statistics/distribution
---
The **chi-square ($\chi^2$) distribution** is a continuous probability distribution that arises when you square independent standard [[Normal Distribution|normal]] [[Set Theory#Random Variable|random variables]] and sum them together.

It forms the backbone of hypothesis testing for categorical data, variance estimation, and model goodness-of-fit. See [[Chi-Square Test]].

If $Z_1, Z_2, \dots, Z_k$ are $k$ independent random variables sampled from a **standard normal distribution** (mean $\mu = 0$, variance $\sigma^2 = 1$), then the sum of their squares follows a chi-square distribution with $k$ degrees of freedom:

$$Q = \sum_{i=1}^{k} Z_i^2 \sim \chi^2(k)$$

### Key Properties

- **Non-negativity:** Because it is built from squared terms, a chi-square variable can never be negative ($Q \ge 0$).
- [[Degrees of Freedom]] ($k$): The single parameter controlling the shape of the distribution. It represents the number of independent normal variables being summed.
- **Mean and Variance:**
    - Mean: $\text{E}[Q] = k$
    - Variance: $\text{Var}(Q) = 2k$
- **Shape Shift:**
    - For small $k$ (e.g., $k = 1, 2$), the curve is heavily skewed right with a peak near zero.
    - As $k$ increases, the distribution becomes progressively smoother and more symmetric. By the [[Central Limit Theorem]], as $k \to \infty$, $\chi^2(k)$ approaches a normal distribution $N(k, 2k)$.

![[Chi-Square Distribution-1791489447406.webp]]