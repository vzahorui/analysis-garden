---
tags:
  - statistics
aliases:
  - standard error
---
Up: [[Hypothesis Testing]]. 

A **sampling distribution** is the [[Probability Distributions|probability distribution]] of a statistic (such as the sample mean $\bar{X}$, sample proportion $\hat{p}$, or sample variance $s^2$) obtained by taking **all possible samples of a fixed size $n$** from a given population.

Instead of describing the individual values in a population, a sampling distribution describes how a calculated statistic varies across repeated samples.

## The Intuition: A Thought Experiment

Imagine you want to know the average height of all adults in a city (the population mean, $\mu$).

1. You take a random sample of $100$ people ($n = 100$) and calculate their mean height: $\bar{X}_1 = 172 \text{ cm}$.
2. You return those people to the population, take a _new_ random sample of $100$ people, and get: $\bar{X}_2 = 170.5 \text{ cm}$.
3. You repeat this $10,000$ times.

If you plot a [[histogram]] of all those sample means $(\bar{X}_1, \bar{X}_2, \bar{X}_3, \dots, \bar{X}_{10000})$, that histogram forms the **sampling distribution of the mean**.

![[Sampling Distribution-1791379598177.webp]]

## Key Properties (from [[Central Limit Theorem]])

For the sampling distribution of the sample mean $\bar{X}$:

1. **Center (Mean):** The mean of all sample means is equal to the true population mean $\mu$.

$$\mu_{\bar{X}} = \mu$$

The sample mean is an unbiased estimator of the population mean.

2. **Spread (Standard Error):** The standard deviation of the sampling distribution is called the **Standard Error ($SE$)**. It measures how much sample estimates fluctuate from sample to sample.
$$\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}}$$

- As sample size $n$ increases, the standard error decreases by a factor of $\sqrt{n}$, meaning larger samples produce tighter, more accurate estimates.

See [[Sampling Distribution#Why Standard Error Divides by $ sqrt{n}$]]

2. **Shape (Central Limit Theorem):** Regardless of the shape of the population distribution (whether skew, uniform, or bimodal), as long as the sample size $n$ is sufficiently large (typically $n \ge 30$), the sampling distribution of the mean approaches a [[Normal Distribution]]:

$$\bar{X} \sim N\left(\mu, \frac{\sigma}{\sqrt{n}}\right)$$

## Why It Matters in Statistics

| **Concept**               | **Role of Sampling Distribution**                                                                                                                    |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Hypothesis Testing]]    | Calculates the probability ($p$-value) of observing a sample statistic as extreme as yours under a null hypothesis.                                  |
| [[Confidence Interval]]   | Provides the standard error needed to construct margin-of-error bounds around point estimates (e.g., $\bar{X} \pm z \cdot \frac{\sigma}{\sqrt{n}}$). |
| **Inference Reliability** | Quantifies uncertainty so decisions are made using probabilistic rigor rather than single-sample guesswork.                                          |

## Sampling Distribution vs Population vs Sample

|**Feature**|**Population Distribution**|**Sample Distribution**|**Sampling Distribution**|
|---|---|---|---|
|**What it contains**|Individual raw observations ($X$) from the entire group|Individual raw observations ($X$) from a single subset|Calculated statistics ($\bar{X}, s^2, \hat{p}$) across repeated samples|
|**Size**|$N$ (Total population size)|$n$ (Sample size)|Infinite (or all possible combinations $\binom{N}{n}$)|
|**Mean symbol**|$\mu$|$\bar{x}$|$\mu_{\bar{X}}$|
|**Standard deviation symbol**|$\sigma$|$s$|$\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}}$ (Standard Error)|

## Why Standard Error Divides by the Square Root of n?

The standard error of the mean ($SE$) measures how much sample means ($\bar{X}$) vary from sample to sample around the true population mean ($\mu$).

To understand where $\sqrt{n}$ comes from mathematically and intuitively, look at how sample observations combine:

#### Step 1: Combining Variances

When taking a random sample of $n$ independent observations $X_1, X_2, \dots, X_n$, each observation comes from a population with variance $\sigma^2$.

The sample mean is defined as:

$$\bar{X} = \frac{X_1 + X_2 + \dots + X_n}{n} = \frac{1}{n} \sum_{i=1}^n X_i$$

Using the variance rule for independent [[Set Theory#Random Variable|random variables]]: $\text{Var}(aX) = a^2 \text{Var}(X)$ and $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y)$:

$$\text{Var}(\bar{X}) = \text{Var}\left(\frac{1}{n} \sum_{i=1}^n X_i\right) = \frac{1}{n^2} \sum_{i=1}^n \text{Var}(X_i)$$

Since each observation $X_i$ comes from the same population with variance $\text{Var}(X_i) = \sigma^2$:

$$\text{Var}(\bar{X}) = \frac{1}{n^2} \left( \underbrace{\sigma^2 + \sigma^2 + \dots + \sigma^2}_{n \text{ times}} \right) = \frac{1}{n^2} (n \sigma^2) = \frac{\sigma^2}{n}$$

#### Step 2: Converting Variance to Standard Deviation

Standard deviation is the square root of variance. Taking the square root of $\text{Var}(\bar{X})$ gives the standard error ($\sigma_{\bar{X}}$):

$$\sigma_{\bar{X}} = \sqrt{\text{Var}(\bar{X})} = \sqrt{\frac{\sigma^2}{n}} = \frac{\sigma}{\sqrt{n}}$$
## Using Sample Standard Deviation s and Bessel's Correction (n-1)

In practice, the true population standard deviation $\sigma$ is almost always unknown. The sample standard deviation $s$ is substituted in its place to estimate the standard error:

$$SE = \frac{s}{\sqrt{n}}$$

Because $s$ itself is an estimate subject to sample variability, the resulting standardized test statistic follows a [[Student's t-Distribution]] with $n - 1$ [[degrees of freedom]] rather than a standard [[Normal Distribution|Normal]] $Z$-distribution (though as $n$ grows large, $t$ converges to $Z$).
### Why divide by $n - 1$? (Bessel's Correction)

When calculating $s$, divide by $n - 1$ rather than $n$:

$$s = \sqrt{\frac{\sum_{i=1}^n (X_i - \bar{X})^2}{n - 1}}$$

There are two main reasons for using $n - 1$:

1. **Correcting Downward Bias:**
    
    Because $\bar{X}$ shifts slightly toward the sample data points compared to where $\mu$ actually lies, calculating $\sum (X_i - \bar{X})^2$ slightly _underestimates_ the true spread around $\mu$. Dividing by $n - 1$ inflates the variance estimate slightly to make $s^2$ an **unbiased estimator** of $\sigma^2$ (meaning $E[s^2] = \sigma^2$).
    
1. [[Degrees of Freedom]]:
    
    To calculate $s$, $\bar{X}$ must first be calculated. The sample mean places a constraint on the data points because their deviations from $\bar{X}$ must sum to zero:
    
    $$\sum_{i=1}^n (X_i - \bar{X}) = 0$$
    
    Once $n - 1$ deviations are known, the $n$-th deviation is fixed and cannot vary freely. Thus, only $n - 1$ independent pieces of information remain to estimate variability.
