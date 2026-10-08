---
tags:
  - statistics
aliases:
  - confidence intervals
---
A **confidence interval (CI)** gives an estimated range of values that likely contains an unknown population parameter (like a mean or percentage), based on data collected from a sample.

Instead of guessing a single number—a **point estimate**, such as _"the average user height is 170 cm"_—a confidence interval gives a range with a measure of certainty: _"We are 95% confident that the true average user height is between 167 cm and 173 cm."_

## Core Components

A confidence interval consists of three main elements:

$$\text{Confidence Interval} = \text{Point Estimate} \pm \text{Margin of Error}$$

1. **Point Estimate:** The sample mean or statistic calculated directly from your sample.
2. **Margin of Error:** The radius of the interval, which depends on two factors:
    
    - **Variability (Standard Error):** How much variation exists in the data and how large your sample is ($SE = \frac{s}{\sqrt{n}}$). See [[Sampling Distribution]].
    - **Confidence Level ($1 - \alpha$):** How certain you want to be (commonly 90%, 95%, or 99%).

**Confidence Level** determines the proportion of times the calculated interval would contain the true population parameter if you repeated the sampling process many times under identical conditions.

## Frequentist Interpretation: The 95% Meaning

The most common misconception is that a 95% confidence interval means _"there is a 95% probability that the true parameter lies within this specific interval."_

In classical (frequentist) statistics:

- The population parameter is a **fixed, fixed-but-unknown constant**—it does not change or move.
- The interval boundaries are **random variables** because they depend on the random sample drawn.
- Therefore, a 95% confidence level means: **If you draw 100 independent random samples and compute a 95% CI for each, roughly 95 of those 100 intervals will capture the true population parameter.**

## Mathematical Formula (Mean of a [[Normal Distribution]])

For a population mean $\mu$ with unknown population standard deviation, estimated by sample standard deviation $s$ over sample size $n$:

$$\text{CI} = \bar{x} \pm t^*_{\alpha/2, n-1} \cdot \left(\frac{s}{\sqrt{n}}\right)$$

Where:
- $\bar{x}$ = Sample mean
- $t^*_{\alpha/2, n-1}$ = Critical value from the [[Student's t-Distribution]] with $n-1$ [[Degrees of Freedom]] for a given confidence level.
- $s/\sqrt{n}$ = Standard Error ($SE$)

### Key Trade-offs

|**Factor**|**Change**|**Effect on Interval Width**|**Reason**|
|---|---|---|---|
|**Confidence Level**|$90\% \rightarrow 95\% \rightarrow 99\%$|**Wider**|Being more certain requires casting a wider net.|
|**Sample Size ($n$)**|Increases|**Narrower**|Larger samples reduce standard error ($\propto 1/\sqrt{n}$).|
|**Data Variance ($\sigma^2$)**|Increases|**Wider**|Higher noise/spread increases uncertainty.|