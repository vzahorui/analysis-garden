---
tags:
  - statistics/test
aliases:
  - homogeneity of variance
  - homoscedasticity
---
**Levene’s test** evaluates whether two or more groups have equal variances in the population, a property known as **homogeneity of variance** (or _homoscedasticity_).

Many common statistical parametric tests, such as [[ANOVA]] or independent samples [[T-test|t-tests]], assume that all groups being compared come from populations with equal variance. Levene’s test checks this assumption before running those primary analyses.

## Hypotheses

See [[Hypothesis Testing]].

- **Null Hypothesis ($H_0$):** The population variances are equal across all groups.

$$\sigma_1^2 = \sigma_2^2 = \dots = \sigma_k^2$$

- **Alternative Hypothesis ($H_1$):** At least one group has a population variance different from the others.

## How It Works

Instead of analyzing the raw data directly, Levene’s test performs a standard one-way ANOVA on the **absolute deviations** of the data points from their group center.

### Step 1: Calculate Deviations

For each observation $x_{ij}$ (observation $i$ in group $j$), compute the absolute distance $z_{ij}$ from a central measure $Z_{\cdot j}$ of group $j$:

$$z_{ij} = \vert{}x_{ij} - Z_{\cdot j}\vert{}$$

Depending on the choice of $Z_{\cdot j}$, there are two common variations:

1. **Original Levene’s Test:** $Z_{\cdot j} = \bar{x}_j$ (the group **mean**).
2. **Brown–Forsythe Test (Robust Levene's):** $Z_{\cdot j} = \tilde{x}_j$ (the group **median**). Using the median makes the test far more robust against outliers and non-normal skewed distributions.

#### Step 2: Compute the Test Statistic ($W$)

Run a standard One-Way ANOVA on the transformed values $z_{ij}$. The test statistic $W$ is calculated as:

$$W = \frac{(N - k)}{(k - 1)} \cdot \frac{\sum_{j=1}^{k} N_j (\bar{z}_{\cdot j} - \bar{z}_{\cdot \cdot})^2}{\sum_{j=1}^{k} \sum_{i=1}^{N_j} (z_{ij} - \bar{z}_{\cdot j})^2}$$
### Step 3: Evaluate Significance

The test statistic $W$ follows an $F$-distribution with $k - 1$ and $N - k$ [[degrees of freedom]].

- **$p$-value $\ge 0.05$:** Fail to reject $H_0$. Group variances are not significantly different (homogeneity of variance holds).
- **$p$-value $< 0.05$:** Reject $H_0$. Group variances differ significantly, violating the homoscedasticity assumption.

### What to Do If Levene's Test Fails ($p < 0.05$)

If Levene's test is significant, you should avoid standard ANOVA or Student's $t$-test. Instead:

1. **For 2 groups:** Use **Welch's $t$-test** [[T-test#Welch's t-test]] instead of the standard independent $t$-test.
2. **For $>2$ groups:** Use [[ANOVA#Welch’s ANOVA]] or **Brown–Forsythe ANOVA** instead of standard One-Way ANOVA.
