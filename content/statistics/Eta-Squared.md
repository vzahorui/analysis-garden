---
tags:
  - statistics
---
**Eta squared** ($\eta^2$) is a measure of [[Effect Size]] used in Analysis of Variance ([[ANOVA]]). While a $p$-value tells you whether a difference between groups is statistically significant, eta squared tells you **how large or practical that difference actually is**.

### What Does Eta Squared Represent?

Eta squared measures the **proportion of variance in the dependent variable explained by an independent variable**.

It works identically to $R^2$ (the coefficient of determination) in [[linear regression]]. An $\eta^2$ value ranges from **0 to 1** (or 0% to 100%):

- **$\eta^2 = 0.00$**: The independent variable explains 0% of the variance (no effect).
- **$\eta^2 = 0.15$**: The independent variable explains 15% of the variance.
- **$\eta^2 = 1.00$**: The independent variable explains 100% of the variance (perfect prediction).

### Mathematical Formula

In a standard one-way ANOVA, $\eta^2$ is calculated by dividing the **Sum of Squares between groups ($SS_{\text{effect}}$)** by the **Total Sum of Squares ($SS_{\text{total}}$)**:

$$\eta^2 = \frac{SS_{\text{between}}}{SS_{\text{total}}}$$

Where:

- **$SS_{\text{between}}$** is the variation caused by your treatment or grouping factor.
- **$SS_{\text{total}}$** is the total variation observed across all data points combined ($SS_{\text{between}} + SS_{\text{within}}$).

### How to Interpret Eta Squared Values

According to Jacob Cohen's widely used guidelines for social sciences and statistics:

|**Value of η2**|**Effect Size Interpretation**|
|---|---|
|**0.01 ($\sim 1\%$)**|**Small** effect|
|**0.06 ($\sim 6\%$)**|**Medium** effect|
|**0.14 ($\sim 14\%$)**|**Large** effect|

> **Example:** Suppose you run an experiment testing three different study methods on exam scores. If your ANOVA yields an $\eta^2 = 0.18$, it means **18% of the difference in exam scores is directly attributable to the study method used**, while the remaining 82% is due to individual differences or measurement error.

### Eta Squared vs. Partial Eta Squared ($\eta_p^2$)

In a **One-Way ANOVA**, eta squared and partial eta squared are identical. However, in **Two-Way or Factorial ANOVAs** with multiple factors, they differ:

- **Eta Squared ($\eta^2$)**: Shares of variance relative to the total variance of the study. All factors share the same denominator ($SS_{\text{total}}$), meaning the $\eta^2$ values of all variables and interaction terms sum to less than or equal to 1.
- **Partial Eta Squared ($\eta_p^2$)**: Measures the effect of a specific variable while removing (controlling for) the variance explained by other independent variables.

### Key Limitations to Keep in Mind

1. **Sample Bias (Overestimation)**: $\eta^2$ is a sample statistic and tends to slightly overestimate the true effect size in the general population, especially with small samples.
2. **Alternative Options**: For smaller sample sizes, **Omega squared ($\omega^2$)** or **Epsilon squared ($\epsilon^2$)** are often preferred because they adjust for sample bias and yield less optimistic estimates.