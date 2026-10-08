---
tags:
  - statistics
aliases:
  - t-tests
  - t-statistic
---
A **t-test** is a statistical test (one of [[Hypothesis Testing#Standard Test Statistics & Methods]]) used to determine if there is a significant difference between the means (averages) of two groups. It helps you decide whether observed differences are real and meaningful or just the result of random chance.

## When and Why to Use a t-Test

You use a t-test when:

- You are comparing **two groups** (or one group against a known benchmark value).
- Your dependent variable is **continuous** (e.g., height, test scores, reaction time, blood pressure).
- Sample sizes are relatively small ($n < 30$), though it works well with larger samples as well.

### The Mechanics: How It Works

Every t-test produces a metric called the **$t$-statistic** which comes from [[Student's t-Distribution|Student's distribution]], which is conceptually calculated as:

$$t = \frac{\text{Difference between group means}}{\text{Variability within groups}}$$

Here variability within groups is effectively the [[Sampling Distribution|standard error]]. 

- **Large $t$-value:** The difference between groups is much larger than the random noise/spread within each group (likely a real effect).
- **Small $t$-value:** The difference between groups is small compared to the noise (likely random chance).

## The Three Types of t-Tests

|**Type of t-Test**|**Best Used For**|**Example Scenario**|
|---|---|---|
|**One-Sample t-Test**|Comparing **one group's mean** against a known standard or benchmark value.|Testing if a new batch of 500g coffee bags actually weighs 500g on average.|
|**Two-Sample Independent t-Test**|Comparing means from **two completely separate groups** of individuals or subjects.|Comparing test scores between Group A (studied online) and Group B (studied in person).|
|**Paired-Samples t-Test**|Comparing **two measurements taken from the exact same subjects** (or matched pairs).|Measuring blood pressure in the _same_ patients before and after taking a medication.|

### One-Sample $t$-Test

You want to know if a sample mean ($\bar{x}$) differs from a target value ($\mu_0$).

$$t = \frac{\bar{x} - \mu_0}{SE_{\bar{x}}} \quad \text{where} \quad SE_{\bar{x}} = \frac{s}{\sqrt{n}}$$

- **Numerator:** Distance between your sample mean and the target.
- **Denominator:** **Standard Error of the Mean ($SE$)**, which measures how much sample means fluctuate from sample to sample due to chance.

### Independent Two-Sample $t$-Test (Equal Variances)

You want to know if the difference between two independent group means ($\bar{x}_1 - \bar{x}_2$) is non-zero.

$$t = \frac{(\bar{x}_1 - \bar{x}_2) - 0}{SE_{(\bar{x}_1 - \bar{x}_2)}} \quad \text{where} \quad SE_{(\bar{x}_1 - \bar{x}_2)} = s_{pooled} \cdot \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}$$

- **Numerator:** Difference between the two group averages.
- **Denominator:** **Standard Error of the Difference Between Means ($SE$)**.

### Paired-Samples $t$-Test

You want to know if the average difference score ($\bar{d}$) between paired measurements differs from zero.

$$t = \frac{\bar{d} - 0}{SE_{\bar{d}}} \quad \text{where} \quad SE_{\bar{d}} = \frac{s_d}{\sqrt{n}}$$

- **Numerator:** Average difference across pairs ($\bar{d}$).
- **Denominator:** **Standard Error of Difference Scores ($SE$)**, calculated as the standard deviation of individual differences ($s_d$) divided by $\sqrt{n}$.

Compared to the case of independent samples, paired test has smaller standard error, and therefore it has more statistical power in rejecting the null hypothesis.

## Key Assumptions of t-Tests

Before running a t-test, make sure your data meets these conditions:

1. **Continuous Scale:** Data is measured on an interval or ratio scale (e.g., weight, speed, score).
2. **Normality:** The data (or differences, in a paired test) should follow a roughly [[Normal Distribution|normal]] (bell-curve) distribution, especially for small samples ($n < 30$).
3. **Random Sampling:** Data should be collected via a representative, random sample.
4. **Equal Variances (Independent t-test only):** Both groups should have roughly equal variance (homogeneity of variance). If violated, use **Welch's t-test**.

## Welch's t-test

Unlike the standard Student's t-test, Welch's t-test does **not** assume that the two groups have equal variances, making it a far more robust choice for real-world data analysis.

#### Welch's Test Statistic ($t$)

Instead of using a pooled variance, Welch's t-test uses unpooled sample variances ($s_1^2, s_2^2$) and sample sizes ($n_1, n_2$):

$$t = \frac{\bar{X}_1 - \bar{X}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$$

#### Welch–Satterthwaite [[Degrees of Freedom]]

Because variances differ, the test statistic no longer follows a standard t-distribution with $n_1 + n_2 - 2$ degrees of freedom. Instead, it uses an adjusted degrees of freedom calculation (often resulting in a non-integer value):

$$\nu \approx \frac{\left( \frac{s_1^2}{n_1} + \frac{s_2^2}{n_2} \right)^2}{\frac{(s_1^2 / n_1)^2}{n_1 - 1} + \frac{(s_2^2 / n_2)^2}{n_2 - 1}}$$

This lower degrees of freedom penalizes for unequal variances, making the test criteria more conservative and maintaining accurate $p$-values.