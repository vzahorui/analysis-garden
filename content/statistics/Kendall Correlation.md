---
tags:
  - statistics
  - EDA
---
Kendall’s correlation evaluates **monotonic** relationships by looking at **pairs of observations** $(x_i, y_i)$ and $(x_j, y_j)$ and assessing whether their directions match across both variables.

It, along with [[Spearman Correlation]], are more robust alternatives to [[Pearson Correlation]] because then deal better with outliers and non-linear data. Kendall’s correlation in particular is more robust in small samples.
## Concordant vs. Discordant Pairs

For any pair of observations $i$ and $j$:
- **Concordant:** Both $x$ and $y$ move in the same direction ($x_i > x_j$ and $y_i > y_j$, OR $x_i < x_j$ and $y_i < y_j$).
- **Discordant:** $x$ and $y$ move in opposite directions ($x_i > x_j$ and $y_i < y_j$, OR $x_i < x_j$ and $y_i > y_j$).
- **Tied:** $x_i = x_j$ or $y_i = y_j$.
## Mathematical Definition

For a dataset with no ties (Kendall's $\tau_a$):

$$\tau = \frac{C - D}{\frac{1}{2} n (n - 1)}$$
- $C$: Number of concordant pairs
- $D$: Number of discordant pairs
- $\frac{1}{2} n(n - 1)$: Total number of distinct pairs among $n$ observations
## When to Use Kendall

- Your sample size is small ($n < 30$).
- The dataset contains many tied ranks.
- Otherwise default to [[Spearman Correlation]] when the relationship is non-linear but monotone.
## Watch for

It doesn't detects U-shaped or other non-monotone patterns. Always pair with a [[Scatter Plot]].