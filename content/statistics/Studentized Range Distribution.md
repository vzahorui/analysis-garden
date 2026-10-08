---
tags:
  - statistics/distribution
---
The **studentized range distribution** (denoted by $q$) is a probability distribution used primarily in post-hoc multiple comparison tests, such as [[ANOVA#Tukey’s HSD (Honestly Significant Difference)]] test.

It models the distribution of the difference between the sample maximum and sample minimum across $k$ independent groups, normalized by an estimate of the sample standard deviation.

## Conceptual Definition

When comparing multiple sample means from $k$ independent [[Normal Distribution|normal]] populations with the same true mean $\mu$ and standard deviation $\sigma$, the absolute difference between the extreme sample means will naturally grow as the number of groups $k$ increases.

To account for this multi-group expansion without increasing false positive rates (Type I errors), the test statistic $q$ scales the sample range by an independent pooled standard error estimate:

$$q = \frac{\bar{X}_{\text{max}} - \bar{X}_{\text{min}}}{s_{\text{pooled}} / \sqrt{n}}$$

Where:

- $\bar{X}_{\text{max}}$ and $\bar{X}_{\text{min}}$ are the largest and smallest sample means among $k$ groups.
- $s_{\text{pooled}} = \sqrt{MS_{\text{error}}}$ is the pooled standard deviation across all groups.
- $n$ is the sample size per group (assuming equal group sizes).

## Key Parameters

The probability density function depends on two main parameters:

1. **Number of groups ($k$):** The total number of independent group means being compared ($k \ge 2$). As $k$ increases, the expected value of $q$ shifts to the right because the range between the minimum and maximum mean expands with more samples.
2. **Degrees of freedom ($\nu$ or $df$):** The degrees of freedom associated with the error variance estimate $s_{\text{pooled}}$ (typically $N - k$, where $N$ is the total sample size across all groups).

## Reading Critical Values ($q$-Tables)

In hypothesis testing, $q_{\text{calc}}$ is compared against a critical value $q_{\alpha, k, \nu}$ from the Studentized Range Table.
