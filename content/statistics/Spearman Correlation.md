---
tags:
  - EDA
  - statistics
---
Spearman's correlation measures how well the relationship between two variables can be described using a monotonic function. It is equivalent to calculating the standard [[Pearson correlation]] on the **ranked values** of the dataset rather than the raw scores.
### Mathematical Definition

If there are no tied ranks, Spearman’s $\rho$ is calculated as:
$$\rho = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}$$
- $d_i = \text{Rank}(x_i) - \text{Rank}(y_i)$: Difference between ranks for pair $i$
- $n$: Number of observations

### When to Use Spearman

- You have continuous data that violates Pearson’s assumption of [[Normal Distribution|normality]] or linearity.
- Your data includes non-linear monotonic patterns (e.g., exponential growth).
- You are analyzing ordinal data (e.g., competition ranks).
- If there are many ties or when the sample is small, better use [[Kendall Correlation]].