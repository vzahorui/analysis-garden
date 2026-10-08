---
tags:
  - statistics
---
A meta-analysis is a statistical technique that pools [[effect size]] estimates across independent studies to calculate a unified weighted average effect.

## Key Elements & Mechanics

1. **Standardized Effect Sizes:** Because studies measure outcomes differently, results are converted to a standardized metric, such as Cohen’s $d$, Hedges’ $g$, or Odds Ratios (OR).
2. **Weighting Scheme:** Larger, more precise studies receive higher weight ($w_i$). The inverse-variance weighting method sets:

$$w_i = \frac{1}{SE_i^2}$$
where $SE_i$ is the [[Sampling Distribution|standard error]] of study $i$.

3. **Pooled Effect Estimate ($\bar{\theta}$):**

$$\bar{\theta} = \frac{\sum (w_i \cdot \theta_i)}{\sum w_i}$$

4. **Forest Plot:** Visualizes the effect size and 95% confidence interval for each study. The bottom summary diamond represents the pooled overall effect.

![[Meta-Analysis-1791402465058.webp]]

## Fixed-Effects vs Random-Effects Models

|**Feature**|**Fixed-Effects Model**|**Random-Effects Model**|
|---|---|---|
|**Assumption**|All studies share one true underlying effect size.|True effect sizes vary across studies due to differing populations/methods.|
|**Variance Source**|Sampling error within studies only ($\sigma_i^2$).|Within-study variance ($\sigma_i^2$) + between-study variance ($\tau^2$).|
|**Weight ($w_i$)**|$\frac{1}{\sigma_i^2}$|$\frac{1}{\sigma_i^2 + \tau^2}$|
