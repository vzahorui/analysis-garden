---
tags:
  - statistics
---
# Hypothesis Testing

> [!info] In one sentence  
> Hypothesis testing is a framework for deciding whether sample data provide enough evidence against a **null hypothesis** to reject it in favor of an **alternative hypothesis**.

Up: [[Statististical Concepts|Statistics]].

Related: [[p-value]], [[Confidence Interval]], [[Effect Size]], [[Statistical Power]], [[Type I and Type II Errors]], [[Sampling Distribution]]

---

## Core Concepts

### 1. Key Terminology & Definitions

- **Null Hypothesis ($H_0$):** The default assumption that there is no effect, no difference, or no relationship between variables. It serves as the baseline model ($H_0: \theta = \theta_0$).
- **Alternative Hypothesis ($H_1$ or $H_a$):** The competing claim that an effect, difference, or relationship exists ($H_a: \theta \neq \theta_0$, $H_a: \theta > \theta_0$, or $H_a: \theta < \theta_0$).
- **Test Statistic:** A standardized numerical summary calculated from sample data that measures how far the sample deviates from what would be expected under $H_0$.
- **Null Distribution:** The theoretical [[sampling distribution]] of the test statistic under the assumption that $H_0$ is true.
- **p-value:** The probability, assuming $H_0$ is true, of obtaining a test statistic at least as extreme as the one observed in the sample data:
    
    $$p\text{-value} = P(\vert{}T\vert{} \ge \vert{}t_0\vert{} \mid H_0)$$
    
- **Significance Level ($\alpha$):** The pre-specified threshold for the p-value below which $H_0$ is rejected (commonly $\alpha = 0.05$ or $0.01$).
    
- **Critical Value ($c$):** The boundary point on the test statistic's distribution corresponding to $\alpha$ that defines the rejection region.​
    
- [[Test Statistic]]
    
- [[Sampling Distribution]]
    
- [[Significance Level]] — αα
    
- [[p-value]]
    
- [[Critical Region]]
    
- [[Decision Rule]]
    
- [[Type I Error]]
    
- [[Type II Error]]
    
- [[Statistical Power]]
    

---

## The logic

1. Assume H0H0​ is true.
    
2. Build a [[Test Statistic]] whose distribution under H0H0​ is known.
    
3. If the observed test statistic is very unlikely under H0H0​, reject H0H0​.
    
4. “Very unlikely” is defined in advance by the [[Significance Level]] αα.
    

A generic test statistic often has the form:

T=θ^−θ0SE(θ^)T=SE(θ^)θ^−θ0​​

where θ^θ^ is an estimate, θ0θ0​ is the null value, and SE(θ^)SE(θ^) is its standard error.

---

## Workflow

> [!tip] Standard hypothesis-testing workflow
> 
> 1. State H0H0​ and H1H1​ in context.
>     
> 2. Choose a test statistic and check its [[Assumptions of Statistical Tests|assumptions]].
>     
> 3. Set αα before looking at the data, e.g. α=0.05α=0.05.
>     
> 4. Collect data and compute the test statistic.
>     
> 5. Compute the [[p-value]] or compare the statistic to the [[Critical Region]].
>     
> 6. Decide:
>     
>     - Reject H0H0​ if p≤αp≤α.
>         
>     - Otherwise, fail to reject H0H0​.
>         
> 7. Interpret in context. Report [[Effect Size]], [[Confidence Interval]], and limitations.
>     

---

## Hypotheses

- H0H0​: usually “no effect”, “no difference”, or “parameter equals a specific value”.
    
    - Example: H0:μ=μ0H0​:μ=μ0​
        
- H1H1​: the effect or difference you want to detect.
    
    - Two-tailed: H1:μ≠μ0H1​:μ=μ0​
        
    - Right-tailed: H1:μ>μ0H1​:μ>μ0​
        
    - Left-tailed: H1:μ<μ0H1​:μ<μ0​
        

Choose H1H1​ before seeing the data. Do not change it after looking at results.

---

## p-value

> [!note] Definition  
> The **p-value** is the probability, assuming H0H0​ is true, of observing a test statistic at least as extreme as the one actually observed.

- Small p-value → data are unusual under H0H0​ → evidence against H0H0​.
    
- p≤αp≤α → reject H0H0​.
    
- p>αp>α → fail to reject H0H0​.
    

> [!warning] What a p-value is not
> 
> - It is **not** the probability that H0H0​ is true.
>     
> - It is **not** the probability that the results are “due to chance alone”.
>     
> - It is **not** a measure of effect size or practical importance.
>     

---

## Decision rule

- **p-value approach:** reject H0H0​ if p≤αp≤α.
    
- **Critical value approach:** reject H0H0​ if the test statistic falls in the rejection region.
    
- **Confidence interval approach:** for a two-sided test, if the null value lies outside the 100(1−α)%100(1−α)% [[Confidence Interval]], reject H0H0​.
    

---

## Errors and power

|Reality|Fail to reject H0H0​|Reject H0H0​|
|---|---|---|
|H0H0​ true|Correct decision, 1−α1−α|[[Type I Error]], αα|
|H0H0​ false|[[Type II Error]], ββ|Correct decision, [[Statistical Power]] =1−β=1−β|

- αα: false positive rate.
    
- ββ: false negative rate.
    
- Power: probability of detecting a true effect.
    
- Power increases with larger effect size, larger sample size, lower variability, and higher αα.
    

See also: [[Power Analysis]]

---

## Assumptions

Every test has assumptions. Common ones:

- [[Independence of Observations]]
    
- [[Normality Assumption]]
    
- [[Homogeneity of Variance]]
    
- [[Random Sampling]]
    
- Measurement scale and model structure
    

If assumptions are violated, consider:

- [[Robust Statistical Methods]]
    
- [[Nonparametric Tests]]
    
- [[Permutation Tests]]
    
- [[Bootstrapping]]
    

---

## Common pitfalls

> [!warning] Common pitfalls
> 
> - “Fail to reject H0H0​” does **not** mean “accept H0H0​”.
>     
> - Statistical significance does **not** imply practical significance.
>     
> - A p-value is not P(H0∣data)P(H0​∣data).
>     
> - Multiple tests inflate Type I error. Use [[Bonferroni Correction]], [[Holm Correction]], or [[False Discovery Rate]].
>     
> - Data peeking and optional stopping invalidate p-values unless pre-planned.
>     
> - Ignoring assumptions can make p-values misleading.
>     
> - A large sample can make tiny, unimportant effects statistically significant.
>     

---

## Effect size and confidence intervals

Hypothesis testing answers “is there evidence?”  
[[Effect Size]] answers “how large is the effect?”  
[[Confidence Interval]] answers “what range of values is plausible?”

Report all three when possible.

Common effect sizes:

- [[Cohen's d]]
    
- [[Pearson's r]]
    
- [[Odds Ratio]]
    
- [[Eta Squared]]
    
- [[R-squared]]
    

---

## Tests by question

### Means

- [[Z-test]]
    
- [[One-sample t-test]]
    
- [[Independent samples t-test]]
    
- [[Paired samples t-test]]
    
- [[One-way ANOVA]]
    
- [[Repeated-measures ANOVA]]
    

### Proportions

- [[One-proportion Z-test]]
    
- [[Two-proportion Z-test]]
    
- [[Chi-squared test]]
    
- [[Fisher's exact test]]
    

### Variances

- [[F-test]]
    
- [[Levene's test]]
    
- [[Bartlett's test]]
    

### Nonparametric

- [[Mann-Whitney U test]]
    
- [[Wilcoxon signed-rank test]]
    
- [[Kruskal-Wallis test]]
    
- [[Friedman test]]
    
- [[Spearman's rank correlation]]
    

### Regression and correlation

- [[t-test for regression coefficients]]
    
- [[F-test for overall regression]]
    
- [[t-test for correlation]]
    

### Bayesian alternatives

- [[Bayes Factor]]
    
- [[Bayesian Hypothesis Testing]]
    

---

## Example

Suppose you want to test whether a population mean differs from 100.

H0:μ=100H0​:μ=100H1:μ≠100H1​:μ=100

You collect a sample, compute:

t=xˉ−100s/nt=s/n​xˉ−100​

If p=0.03p=0.03 and α=0.05α=0.05, you reject H0H0​.  
Then interpret in context and report the mean difference, [[Confidence Interval]], and [[Effect Size]].

---

## See also

- [[Statistical Inference MOC]]
    
- [[Estimation]]
    
- [[Confidence Interval]]
    
- [[p-value]]
    
- [[Statistical Power]]
    
- [[Effect Size]]
    
- [[Type I and Type II Errors]]
    
- [[Multiple Comparisons Problem]]
    
- [[Equivalence Testing]]
    
- [[Permutation Test]]
    
- [[Bayesian Hypothesis Testing]]