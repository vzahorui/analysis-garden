---
tags:
  - statistics/test
---
A **permutation test** (also known as a randomization or re-randomization test) is a non-parametric statistical method used to determine whether an observed effect or difference between groups is [[Hypothesis Testing|statistically significant]].

Instead of relying on theoretical [[Probability Distributions]] (like the standard [[Normal Distribution|Normal]], [[Student's t-Distribution|t]], or $F$ distributions) and strict distributional assumptions, permutation tests calculate the exact (or empirical) probability distribution directly from the observed sample data by shuffling (permuting) group labels.

## The Null Hypothesis

The null hypothesis ($H_0$) in a permutation test typically states that **there is no effect, no relationship, or no difference between the groups**, meaning the group labels assigned to the data points are completely arbitrary and interchangeable.

If $H_0$ is true, shuffling the labels across the dataset should produce test statistics (like the difference in group means) that are just as likely to occur as the test statistic calculated from your original, un-shuffled data.

## How a Permutation Test Works

1. **Calculate the Observed Statistic:**
    
    Compute the test statistic of interest from your real dataset (e.g., difference in means: $\Delta_{\text{obs}} = \bar{X}_A - \bar{X}_B$).
    
2. **Pool the Data:**
    
    Combine the observations from all groups into a single combined dataset, ignoring group assignments.
    
3. **Shuffle and Reassign (Permute):**
    
    Randomly shuffle the combined data points and split them back into pseudo-groups with the original sample sizes.
    
4. **Recalculate the Statistic:**
    
    Compute the test statistic (e.g., $\Delta_{\text{perm}}$) on this shuffled dataset.
    
5. **Repeat:**
    
    Iterate steps 3 and 4 many times (typically 10,000+ times) to build an **empirical null distribution** of the test statistic under $H_0$.
    
6. **Calculate the $p$-value:**
    
    Determine the proportion of permuted test statistics that are as extreme as or more extreme than the observed statistic $\Delta_{\text{obs}}$:
    
    $$p\text{-value} = \frac{\text{Number of permutations where } \vert{}\Delta_{\text{perm}}\vert{} \ge \vert{}\Delta_{\text{obs}}\vert{}}{\text{Total number of permutations}}$$


### Key Properties & Advantages

- **Distribution-Free:** Does not assume normality, equal variances, or specific population parameters.
- **Exact vs Monte Carlo Approximation:**
    
    - **Exact Permutation Test:** Evaluates every possible permutation ($N!$). Practical for small sample sizes.
    - **Monte Carlo / Approximation Permutation Test:** Randomly samples a large number of permutations (e.g., $10,000$). Practical for larger datasets.
        
- **Flexibility:** Can be applied to virtually any test statistic (means, medians, variance ratios, $R^2$, spatial autocorrelation metrics, custom metrics).

### Key Assumptions

While permutation tests are flexible and non-parametric, they are not completely assumption-free:

1. **Exchangeability under $H_0$:** The observations must be exchangeable under the null hypothesis. This implies that observations are independent and identically distributed (i.i.d.) across groups if $H_0$ holds.
2. **Independence:** Observations must be independent of one another (unless the permutation scheme explicitly accounts for structured data, such as paired samples or time-series blocks).