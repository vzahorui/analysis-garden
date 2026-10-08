---
tags:
  - statistics
  - statistics/test
---
Statistical power ($1 - \beta$) is the probability that a study will correctly detect a real effect when one exists (i.e., avoiding a false negative or Type II error). A power analysis calculates the minimum **sample size** required before running an experiment with [[Hypothesis Testing|hypothesis test]].

It balances four tightly linked parameters:

- **Statistical Power ($1 - \beta$):** Typically set to 0.80 (80%), meaning an 80% chance of detecting a true effect.
- **Significance Level ($\alpha$):** The false positive threshold, typically set to 0.05 (5%).
- [[Effect Size]] ($d$, $r$, or $\eta^2$): The expected magnitude or magnitude of interest of the effect (e.g., Cohen's $d = 0.5$ for a medium effect).
- **Sample Size ($N$):** The number of participants or observations needed.

## Core Formula Relationship

For a standard two-sample [[t-test]] comparing two means with equal group sizes ($n$), the required sample size per group is approximated by:

$$n \approx 2 \cdot \left( \frac{Z_{1 - \alpha/2} + Z_{1 - \beta}}{d} \right)^2$$

Where:

- $Z_{1 - \alpha/2}$ is the critical $Z$-value for the significance level (1.96 for $\alpha = 0.05$).
- $Z_{1 - \beta}$ is the $Z$-value for the target power (0.84 for 80% power).
- $d$ is Cohen’s effect size ($\frac{\mu_1 - \mu_2}{\sigma}$).

### Derivation

#### 1. Setup the Hypotheses and Test Statistic

We want to compare two population means $\mu_1$ and $\mu_2$ with known population standard deviation $\sigma$.

- **Null Hypothesis ($H_0$):** $\mu_1 - \mu_2 = 0$
- **Alternative Hypothesis ($H_1$):** $\mu_1 - \mu_2 = \delta$ (where $\delta = \mu_1 - \mu_2 \neq 0$ is the true mean difference)

Let $\bar{X}_1$ and $\bar{X}_2$ be the sample means from two independent samples of size $n$. The [[Variance of a Difference|difference]] between sample means $\bar{D} = \bar{X}_1 - \bar{X}_2$ has [[Sampling Distribution|standard error]]:

$$\text{SE}(\bar{D}) = \sqrt{\frac{\sigma^2}{n} + \frac{\sigma^2}{n}} = \sigma \sqrt{\frac{2}{n}}$$

#### 2. Significance Criterion (Under $H_0$)

Under the null hypothesis ($H_0$), the test statistic follows a standard [[normal distribution]]:

$$Z = \frac{\bar{D} - 0}{\sigma \sqrt{\frac{2}{n}}} \sim \mathcal{N}(0, 1)$$

For a two-tailed test with significance level $\alpha$, we reject $H_0$ if the absolute observed difference exceeds the critical boundary:

$$\vert{}\bar{D}_{\text{crit}}\vert{} = Z_{1 - \alpha/2} \cdot \sigma \sqrt{\frac{2}{n}}$$

#### 3. Power Criterion (Under $H_1$)

Under the alternative hypothesis ($H_1$), the sample difference is normally distributed around the true effect size $\delta$:

$$\bar{D} \sim \mathcal{N}\left(\delta, \sigma^2 \frac{2}{n}\right)$$

Assuming without loss of generality that $\delta > 0$, power ($1 - \beta$) is the probability that our sample difference falls into the upper rejection region ($\bar{D} \ge \bar{D}_{\text{crit}}$):

$$P(\bar{D} \ge \bar{D}_{\text{crit}} \mid H_1) = 1 - \beta$$

Standardizing $\bar{D}_{\text{crit}}$ under $H_1$:

$$Z_{\text{power}} = \frac{\bar{D}_{\text{crit}} - \delta}{\sigma \sqrt{\frac{2}{n}}}$$

Because the lower-tail probability of standard normal variable up to $-Z_{1-\beta}$ equals $\beta$, the critical cutoff must be $Z_{1-\beta}$ standard errors below the mean $\delta$:

$$\bar{D}_{\text{crit}} = \delta - Z_{1 - \beta} \cdot \sigma \sqrt{\frac{2}{n}}$$

#### 4. Equating the Cutoff Values

Equating the expressions for $\bar{D}_{\text{crit}}$ from Step 2 and Step 3:

$$Z_{1 - \alpha/2} \cdot \sigma \sqrt{\frac{2}{n}} = \delta - Z_{1 - \beta} \cdot \sigma \sqrt{\frac{2}{n}}$$

Rearranging terms to isolate $\delta$:

$$\delta = \left( Z_{1 - \alpha/2} + Z_{1 - \beta} \right) \sigma \sqrt{\frac{2}{n}}$$

#### 5. Solving for $n$

Divide both sides by $\sigma$:

$$\frac{\delta}{\sigma} = \left( Z_{1 - \alpha/2} + Z_{1 - \beta} \right) \sqrt{\frac{2}{n}}$$

Substitute Cohen's $d = \frac{\delta}{\sigma}$:

$$d = \left( Z_{1 - \alpha/2} + Z_{1 - \beta} \right) \sqrt{\frac{2}{n}}$$

Rearrange to isolate $\sqrt{n}$:

$$\sqrt{n} = \frac{\sqrt{2} \cdot \left( Z_{1 - \alpha/2} + Z_{1 - \beta} \right)}{d}$$

Squaring both sides yields the final equation:

$$n = 2 \cdot \left( \frac{Z_{1 - \alpha/2} + Z_{1 - \beta}}{d} \right)^2$$


