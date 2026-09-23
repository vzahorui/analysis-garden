---
tags:
  - statistics/test
  - statistics/distribution
---
The **Kolmogorov-Smirnov (K-S) test** is a non-parametric [[Statistical Test]] used to evaluate whether a sample comes from a specific continuous distribution, or whether two independent samples come from the same underlying [[Probability Distributions|distribution]].

Unlike tests that compare summary metrics like means (t-test) or variances (F-test), the K-S test evaluates the **entire shape of the cumulative distribution function (CDF)**.

## Core Concept: The Test Statistic ($D$)

The K-S test measures the **maximum vertical distance** ($D$) between two Cumulative Distribution Functions (CDFs):

1. **One-Sample K-S Test:** Compares the empirical cumulative distribution function (ECDF) of an observed sample $F_n(x)$ against a reference theoretical CDF $F_0(x)$.
$$D = \sup_x \vert{}F_n(x) - F_0(x)\vert{}$$
2. **Two-Sample K-S Test:** Compares the ECDFs of two independent samples, $F_{1, n_1}(x)$ and $F_{2, n_2}(x)$.
$$D = \sup_x \vert{}F_{1, n_1}(x) - F_{2, n_2}(x)\vert{}$$
If the observed maximum distance $D$ exceeds a critical value for a given sample size and significance level ($\alpha$), or if the resulting p-value is less than $\alpha$, the null hypothesis ($H_0$) is rejected.

