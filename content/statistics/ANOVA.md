---
tags:
  - statistics
---
**ANOVA** (Analysis of Variance) is a statistical technique used to compare the means of **three or more groups** to determine if at least one group is significantly different from the others.

## Why Not Just Use Multiple t-Tests?

If you want to compare two groups, a standard [[t-test]] works fine. But if you have three groups (A, B, and C) and run individual $t$-tests (A vs. B, B vs. C, A vs. C), you encounter the **multiplicity problem** (see [[Multiple Hypothesis Testing#The Multiple Testing Problem]]):

- Every time you perform a hypothesis test at a significance level of $\alpha = 0.05$, there is a 5% chance of finding a false positive (Type I error).
- Running 3 separate tests increases your overall false positive rate to about $1 - (0.95)^3 \approx 14.3\%$.
- ANOVA solves this by testing **all groups simultaneously** in a single test, keeping the overall false positive rate at 5%.

## The Core Intuition: Comparing Two Types of Variance

Despite testing for differences in _means_, ANOVA works by analyzing and comparing two sources of **variance**:

$$\text{Total Variance} = \text{Variance Between Groups} + \text{Variance Within Groups}$$

1. **Between-Group Variance (Signal):** How far apart are the sample means of each group from the overall average?
2. **Within-Group Variance (Noise):** How much scatter/spread exists inside each individual group?

ANOVA calculates the **$F$-statistic**, which is simply the ratio of these two variances:

$$F = \frac{\text{Between-Group Variance (Signal)}}{\text{Within-Group Variance (Noise)}} = \frac{MS_{\text{between}}}{MS_{\text{within}}}$$

- **If $F \approx 1$:** The difference between groups is no larger than random chance/noise.
- **If $F \gg 1$:** The variation between groups is significantly larger than internal noise, suggesting at least one group mean is truly different.

## Types of ANOVA

|**Type**|**Predictor Variables (Factors)**|**Example**|
|---|---|---|
|**One-Way ANOVA**|1 Factor (with $\ge 3$ levels)|Testing test scores across 3 teaching methods (Method A, B, C).|
|**Two-Way ANOVA**|2 Factors|Testing test scores across 3 teaching methods AND student gender.|
|**Repeated Measures ANOVA**|1 Factor measured over time|Measuring patient blood pressure before, immediately after, and 1 month post-treatment.|
|**MANOVA**|$\ge 1$ Factor on **multiple dependent variables**|Testing teaching methods on both math scores AND reading scores simultaneously.|

## The Hypotheses

For a One-Way ANOVA with $k$ groups:

- **Null Hypothesis ($H_0$):** All group means are equal.

$$\mu_1 = \mu_2 = \dots = \mu_k$$

- **Alternative Hypothesis ($H_a$):** At least one group mean is different from the others.

## Key Assumptions

For ANOVA results to be valid, your data should meet four core conditions:

1. **Independence:** Observations within and between groups must be independent of each other.
2. **Normality:** The random variable should be roughly [[Normal Distribution|normally distributed]] within each group.
3. **Homogeneity of Variances (Homoscedasticity):** The variances within each group should be roughly equal (can be tested using [[Levene's test]]).
4. **Continuous Outcome:** The dependent variable is measured on an interval or ratio scale.

## F-Statistic Formula

To calculate the $F$-statistic for a One-Way ANOVA, we break down the total variance into components: **Sum of Squares (SS)**, [[Degrees of Freedom]] ($df$)**, and Mean Squares (MS)**.

### 1. Notation & Setup

Let:

- $k$ = total number of groups
- $N$ = total number of observations across all groups ($N = \sum n_j$)
- $n_j$ = sample size of group $j$
- $X_{ij}$ = individual observation $i$ in group $j$
- $\bar{X}_j$ = mean of group $j$
- $\bar{X}$ = overall grand mean of all observations combined ($\bar{X} = \frac{\sum \sum X_{ij}}{N}$)

### 2. The Complete Formula

$$F = \frac{MS_{\text{between}}}{MS_{\text{within}}} = \frac{SS_{\text{between}}}{df_{\text{between}}} \div \frac{SS_{\text{within}}}{df_{\text{within}}}$$

Expanding each term completely gives:

$$F = \frac{\sum_{j=1}^{k} n_j (\bar{X}_j - \bar{X})^2}{k - 1} \div \frac{\sum_{j=1}^{k} \sum_{i=1}^{n_j} (X_{ij} - \bar{X}_j)^2}{N - k}$$

## Welch’s ANOVA

Standard One-Way ANOVA calculates a global mean and assumes that every group has the exact same population variance ($\sigma_1^2 = \sigma_2^2 = \dots = \sigma_k^2$). When variances differ significantly, standard ANOVA's error term becomes biased, leading to an inflated **Type I error rate** (false positive rate).

Welch’s ANOVA fixes this through two key adjustments:

1. **Weighted Group Means:** Instead of weighting each group mean equally or purely by sample size $n_j$, Welch's test weights each group's mean by the reciprocal of its variance-to-sample-size ratio ($w_j = n_j / s_j^2$). Groups with higher variance contribute less to the overall metric because their estimation is less precise.
2. **Adjusted Degrees of Freedom:** The denominator degrees of freedom ($df_2$) are calculated using a complex formula (Welch–Satterthwaite approximation) based on individual group variances and sample sizes, rather than relying on a fixed total $N - k$.



#### The Test Statistic

The adjusted $F$-statistic ($F_W$) is compared against an $F$-distribution with $df_1 = k - 1$ and the adjusted $df_2$:

$$F_W = \frac{\frac{1}{k-1} \sum_{j=1}^{k} w_j (\bar{x}_j - \bar{x}')^2}{1 + \frac{2(k-2)}{k^2 - 1} \sum_{j=1}^{k} \frac{1}{n_j - 1} \left(1 - \frac{w_j}{W}\right)^2}$$

Where $w_j = \frac{n_j}{s_j^2}$, $W = \sum w_j$, and $\bar{x}' = \frac{\sum w_j \bar{x}_j}{W}$.

## What Happens After ANOVA? (Post-Hoc Analysis)

A significant ANOVA result ($p < 0.05$) tells you that _at least one group is different_, but **it does not tell you which specific group differs**.

To pinpoint the exact differences without inflating error rates, you run a **Post-Hoc Test**:

- **Tukey's HSD (Honestly Significant Difference):** Best when group sizes and variances are equal.
- Games-Howell: Robubust to varying variance. 
- [[Multiple Hypothesis Testing#False Discovery Rate (FDR) & The Benjamini-Hochberg Procedure]] when you have many groups. 

### Tukey’s HSD (Honestly Significant Difference)

Tukey’s HSD calculates a single critical difference threshold. If the absolute difference between any two group means exceeds this threshold, the pair is declared statistically significant.

#### Assumptions

- Equal variances across all groups (Homoscedasticity).
- Equal (or approximately equal) group sample sizes ($n_1 = n_2 = \dots = n_k = n$).

#### Formula

$$\text{HSD} = q_{\alpha, k, df_{\text{within}}} \times \sqrt{\frac{MS_{\text{within}}}{n}}$$

Where:

- **$q_{\alpha, k, df_{\text{within}}}$:** Critical value from the [[Studentized Range Distribution]] at significance level $\alpha$, for $k$ groups, and $df_{\text{within}} = N - k$ degrees of freedom.
- **$MS_{\text{within}}$:** Pooled within-group variance from the overall ANOVA model:
- **$n$:** Sample size per group (if group sizes differ slightly, $n$ is replaced by the harmonic mean $n_h = \frac{k}{\sum \frac{1}{n_j}}$, known as the Tukey-Kramer adjustment).

#### Test Decision

For any pair of groups $i$ and $j$:

$$\text{Reject } H_0 \text{ if } \vert{}\bar{X}_i - \bar{X}_j\vert{} \ge \text{HSD}$$

Alternatively, expressed as a test statistic ($q_{\text{calc}}$):

$$q_{\text{calc}} = \frac{\vert{}\bar{X}_i - \bar{X}_j\vert{}}{\sqrt{\frac{MS_{\text{within}}}{n}}} \ge q_{\alpha, k, df_{\text{within}}}$$

### Games-Howell Test

Games-Howell is a non-parametric-like modification of Tukey’s test designed specifically for situations where group variances are **unequal** ($\sigma_i^2 \neq \sigma_j^2$) and sample sizes are **unbalanced** ($n_i \neq n_j$).

Instead of using a single global $MS_{\text{within}}$ and sample size $n$, Games-Howell calculates a **pair-specific standard error** and **pair-specific Welch-Satterthwaite degrees of freedom** for every individual pairwise comparison.

#### Formula

For comparing group $i$ and group $j$:

$$\text{Critical Difference}_{ij} = q_{\alpha, k, df_{ij}} \times \sqrt{\frac{1}{2} \left( \frac{s_i^2}{n_i} + \frac{s_j^2}{n_j} \right)}$$

Where:

- **$s_i^2$ and $s_j^2$:** Individual sample variances of group $i$ and group $j$
- **$q_{\alpha, k, df_{ij}}$:** Critical value from the Studentized Range Distribution evaluated at the **pair-specific degrees of freedom ($df_{ij}$)**.

#### Test Decision

For groups $i$ and $j$:

$$\text{Reject } H_0 \text{ if } \vert{}\bar{X}_i - \bar{X}_j\vert{} \ge \text{Critical Difference}_{ij}$$

Alternatively, written as a calculated $q$-statistic:

$$q_{\text{calc}} = \frac{\vert{}\bar{X}_i - \bar{X}_j\vert{}}{\sqrt{\frac{1}{2} \left( \frac{s_i^2}{n_i} + \frac{s_j^2}{n_j} \right)}} \ge q_{\alpha, k, df_{ij}}$$