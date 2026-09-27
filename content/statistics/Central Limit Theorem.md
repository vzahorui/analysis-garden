---
tags:
  - statistics
---
The **Central Limit Theorem (CLT)** states that when you take sufficiently large random samples from any population, the distribution of the sample means ($\bar{X}$) will approximate a [[normal distribution]] regardless of the shape of the underlying population distribution.

![[Central Limit Theorem-1790443230784.webp]]

## Core Mathematical Principles

For independent and identically distributed (i.i.d.) random variables $X_1, X_2, \dots, X_n$ with mean $\mu$ and finite variance $\sigma^2$, as the sample size $n \to \infty$:

$$\bar{X}_n \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)$$

Equivalently, the standardized sample mean converges in distribution to the standard normal distribution $\mathcal{N}(0, 1)$:

$$Z = \frac{\bar{X}_n - \mu}{\sigma / \sqrt{n}} \xrightarrow{d} \mathcal{N}(0, 1)$$
### Key Components

- **Center ($\mu$):** The mean of the sampling distribution equals the true population mean.
- **Spread ($\sigma / \sqrt{n}$):** The standard error decreases as $n$ increases, causing the bell curve to become taller and narrower.
- **Sample Size Rule of Thumb:** In practice, $n \ge 30$ is often sufficient for the sampling distribution to approximate a normal distribution. Heavily skewed data may require larger samples.

## Why It Matters

The CLT is the foundational pillar of parametric inferential statistics. Because sample means follow a predictable normal distribution:

1. **[[AB Testing]] & Experiments:** You can perform $z$-tests or $t$-tests to compare two groups without knowing the exact distribution of individual user actions.
2. **[[Confidence Intervals]]:** You can construct margin-of-error bounds around a sample mean using standard normal critical values ($z$-scores).
3. **Opinion Polling:** A survey of 1,000 voters accurately estimates national sentiment because the distribution of sample proportions is approximately normal