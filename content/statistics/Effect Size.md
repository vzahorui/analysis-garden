---
tags:
  - statistics
  - statistics/test
---
> [!info] In one sentence  
An **effect size** is a quantitative measure of the magnitude of a phenomenon — how large a difference, association, or effect actually is, independent of sample size.

## Why effect size matters

A [[Hypothesis Testing|hypothesis test]] answers _whether_ an effect exists. It does **not** answer _how large_ the effect is. Two problems follow:

1. **Sample size drives significance.** With a large enough $n$, even a trivial difference yields a small p-value.
2. **p-values are not comparable across studies.** A p-value depends on sample size, variability, and effect size all at once.

Effect size isolates the magnitude. It is what you compare across studies, what you use in [[Power Analysis]], and what you pool in [[Meta-analysis]].

> [!warning] Statistical significance ≠ practical significance  
> Always interpret effect size in the context of the domain. A "large" effect in one field may be trivial in another.

## Common Types of Effect Size

Effect sizes fall into two main families: **Differences between groups** (standardized mean differences) and **Associations between variables** (variance explained or correlations).

### Group Differences ($d$-family)

Used when comparing two groups (e.g., control vs. treatment, A/B testing).

- **Cohen's $d$**: Measures how many standard deviations apart two group means are.

$$\text{Cohen's } d = \frac{\bar{X}_1 - \bar{X}_2}{s_{\text{pooled}}}$$

$$s_{\text{pooled}} = \sqrt{\frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}}$$

Unlike [[T-test|t-statistic]], $s_{\text{pooled}}$ is an estimation of the global variance, not a [[Sampling Distribution|standard error]]. It does not depend of a sample size.

These are the typical readings of Cohen's $d$: 
- **$0.2$**: Small effect (hard to see without statistics)   
- **$0.5$**: Medium effect (noticeable to a trained observer)
- **$0.8+$**: Large effect (obviously noticeable)

### Associations & Variance Explained ($r$-family)

Used when examining relationships between continuous variables or proportions of variance.

- [[Pearson Correlation]]: Correlation coefficient ($0$ to $\pm1$).
    - $r = 0.10$ (small), $r = 0.30$ (medium), $r = 0.50$ (large)

- **$R^2$ (Coefficient of Determination)**: Percentage of variance in the outcome variable explained by the model.
- **[[Eta-Squared]] ($\eta^2$) / Partial $\eta^2$**: Percentage of total variance explained by a factor in [[ANOVA]] settings.