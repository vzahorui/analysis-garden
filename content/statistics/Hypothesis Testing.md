---
tags:
  - statistics
aliases:
  - hypothesis test
  - statistically significant
---
# Hypothesis Testing

> [!info] In one sentence  
> Hypothesis testing is a framework for deciding whether sample data provide enough evidence against a **null hypothesis** to reject it in favor of an **alternative hypothesis**.

## Key Terminology & Definitions

- **Null Hypothesis ($H_0$):** The default assumption that there is no effect, no difference, or no relationship between variables. It serves as the baseline model ($H_0: \theta = \theta_0$).
- **Alternative Hypothesis ($H_1$ or $H_a$):** The competing claim that an effect, difference, or relationship exists ($H_a: \theta \neq \theta_0$, $H_a: \theta > \theta_0$, or $H_a: \theta < \theta_0$). 
- **Test Statistic:** A standardized numerical summary calculated from sample data that measures how far the sample deviates from what would be expected under $H_0$.

    A generic test statistic often has the form:
    $$T = \frac{\hat \theta - \theta}{SE(\hat\theta)}$$

    where 
    * $\hat \theta$ is an estimate
    * $\theta$  is the null value
    * $SE(\hat\theta)$ is its [[Sampling Distribution|standard error]] of the estimate.

- **Null Distribution:** The theoretical [[sampling distribution]] of the test statistic under the assumption that $H_0$ is true.
- **p-value:** The probability, assuming $H_0$ is true, of obtaining a test statistic at least as extreme as the one observed in the sample data:

$$p\text{-value} = P(\vert{}T\vert{} \ge \vert{}t_0\vert{} \mid H_0)$$

![[Hypothesis Testing-1791382976615.webp]]

- **Significance Level ($\alpha$):** The pre-specified threshold for the p-value below which $H_0$ is rejected (commonly $\alpha = 0.05$ or $0.01$).
- **Critical Value ($c$):** The boundary point on the test statistic's distribution corresponding to $\alpha$ that defines the rejection region.

## The logic

1. Assume $H_0$ is true.
2. Build a **Test Statistic** whose distribution under $H_0$ is known.
3. If the observed test statistic is very unlikely under $H_0$​, reject $H_0$.
4. “Very unlikely” is defined in advance by the Significance Level. 

## General Workflow

1. **Formulate Hypotheses:** State $H_0$ and $H_a$ clearly before looking at the data to prevent [[Confirmation Bias]].
2. **Select Significance Level ($\alpha$):** Fix the threshold for Type I Error prior to testing.
3. **Choose Test & Check Assumptions:** Select the test statistic based on data type, distribution, and sample size, verifying assumptions (e.g., independence, [[Normal Distribution|normality]]).
4. **Compute Test Statistic & p-value:** Calculate the standardized metric, whose distribution under $H_0$ ​ is known, and its corresponding p-value or critical region. 
5. **Make Decision & Interpret:**
    - If $p\text{-value} \le \alpha$ (or $T_{\text{obs}} \in \text{Rejection Region}$): **Reject $H_0$**.
    - If $p\text{-value} > \alpha$: **Fail to reject $H_0$** (never "accept" $H_0$).
6. Interpret in context. Report [[Effect Size]], [[Confidence Interval]], and limitations.

### Effect size and confidence intervals

* Hypothesis testing answers “is there evidence?”  
* [[Effect Size]] answers “how large is the effect?”  
* [[Confidence Interval]] answers “what range of values is plausible?”

Report all three whenever possible.

## Assumptions

Every test, especially parametric one, has assumptions. Common ones:

- Independence of Observations
- [[Normal Distribution|Normality]]
- [[Levene's Test|Homogeneity of Variance]]
- Random Sampling
- Measurement scale and model structure

If assumptions are violated, consider:

- Robust Statistical Methods
- Non-parametric Tests
- [[Permutation Tests]]
- [[Bootstrapping]]

## Decision Matrix & Error Types

| **Truth / Decision** | **Fail to Reject $H_0$**        | **Reject $H_0$ ​**                                |
| -------------------- | ------------------------------- | ------------------------------------------------- |
| **$H_0$ is True**    | Correct Decision ($1 - \alpha$) | **Type I Error** ($\alpha$)                       |
| **$H_0$ is False**   | **Type II Error** ($\beta$)     | Correct Decision ($1 - \beta$, Statistical Power) |

- **Type I Error ($\alpha$):** False Positive. Rejecting $H_0$ when it is actually true.
- **Type II Error ($\beta$):** False Negative. Failing to reject $H_0$ when $H_a$ is true.
- **Statistical Power ($1 - \beta$):** The probability of correctly rejecting $H_0$ when a true effect exists.

See also: [[Power Analysis]].

## Standard Test Statistics & Methods

- [[Z-Test]]: Used for population means or proportions when sample size is large or population variance ($\sigma^2$) is known.
- [[T-test]]:  Used for small sample sizes with unknown population variance (One-sample, Two-sample independent, Paired).
- [[Chi-Square Test]]: Used for categorical data (Goodness-of-fit, Independence, Homogeneity).
- [[McNemar's Test]]: for testing the difference in paired binary nominal outcomes.
- [[ANOVA]]: Analysis of Variance; extends the t-test to compare means across three or more groups.
- Non-Parametric Tests: Distribution-free alternatives (e.g., [[Mann-Whitney U Test|Mann-Whitney U]], Wilcoxon Signed-Rank, Kruskal-Wallis) when normality assumptions fail.

## Key Caveats & Limitations

- **P-value vs. [[Effect Size]]:** A p-value only indicates statistical significance, not practical significance. Always report effect size metrics alongside test statistics (e.g., Cohen's $d$).
- [[Multiple Hypothesis Testing#The Multiple Testing Problem]] Performing multiple simultaneous tests inflates the overall Type I error rate, requiring adjustments like [[Multiple Hypothesis Testing#False Discovery Rate (FDR) & The Benjamini-Hochberg Procedure]]. 
- **Sample Size Dependence:** Extremely large sample sizes can yield tiny p-values for trivial effect sizes, whereas small samples may suffer from low **Statistical Power**.
