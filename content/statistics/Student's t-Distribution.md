---
tags:
  - statistics
aliases:
  - t-distribution
  - Student's distribution
---
Up: [[Probability Distributions]].

The **Student’s $t$-distribution** is a probability distribution used in [[Statististical Concepts|Statistics]] when estimating the mean of a [[Normal Distribution|normally distributed]] population when the sample size is small and the true population standard deviation ($\sigma$) is unknown.

## Why Do We Need It?

When you know the true population standard deviation $\sigma$, you use the standard normal distribution ($Z$-distribution) to calculate [[Confidence Interval|confidence intervals]] and perform $z$-tests:

$$Z = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}}$$

In practice, you almost never know $\sigma$. Instead, you estimate it using the sample standard deviation ($s$):

$$t = \frac{\bar{X} - \mu}{s / \sqrt{n}}$$

Because $s$ varies from sample to sample, substituting $s$ for $\sigma$ adds extra uncertainty. The $t$-distribution explicitly accounts for this extra variance by having **heavier tails** than the [[Normal Distribution]], making extreme values more likely when sample sizes are small.

## Core Characteristics

|**Feature**|**Description**|
|---|---|
|**Shape**|Symmetric, bell-shaped, and centered at zero (like the normal distribution).|
|**Tails**|Wider/flatter than the normal distribution, giving higher probability to tail events.|
|**Degrees of Freedom ($\nu$ or $df$)**|The single parameter defining its shape, equal to $n - 1$ for single-sample estimates.|
|**Convergence**|As $df \to \infty$, the $t$-distribution becomes identical to the standard normal distribution $\mathcal{N}(0, 1)$.|

![[Student's t-Distribution-1791383649210.webp]]

## Common Applications

1. [[Hypothesis Testing]]: using for test statistic distribution, in particular [[T-test]]:
    * ***One-Sample $t$-test:** Testing whether a sample mean significantly differs from a hypothesized population mean.
    * **Two-Sample $t$-test:** Comparing the means of two independent groups (e.g., control vs. treatment).
    * **Paired $t$-test:** Comparing paired measurements on the same subjects (e.g., pre-test vs. post-test).
2. [[Confidence Interval|Confidence Intervals]]: Constructing bounds around a sample mean when $\sigma$ is unknown:

$$\bar{X} \pm t_{\alpha/2, \, n-1} \left(\frac{s}{\sqrt{n}}\right)$$
3.  [[Linear Regression]]: Testing the statistical significance of regression coefficients.