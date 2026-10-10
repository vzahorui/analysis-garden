---
tags:
  - statistics/test
aliases:
  - McNemar
---
McNemar’s test evaluates whether there is a significant change or difference in **paired binary nominal outcomes**.

Where a standard [[Chi-Square test]] compares two _independent_ groups, McNemar’s test is designed specifically for **matched or paired data**, such as testing the same subject before and after an intervention, or comparing two diagnostic algorithms evaluated on the exact same dataset.

## The $2 \times 2$ Contingency Table

Data for McNemar's test is arranged in a $2 \times 2$ matrix reflecting the outcomes under two conditions (e.g., _Before_ vs. _After_, or _Model A_ vs. _Model B_):

| Before/After                |**After: Pass / Positive**|**After: Fail / Negative**|
|---|---|---|
| **Before: Pass / Positive** |$a$ (Concordant)|$b$ (Discordant)|
| **Before: Fail / Negative** |$c$ (Discordant)|$d$ (Concordant)|

- **Concordant pairs ($a$ and $d$):** Subjects whose outcome remained unchanged. These carry **no information** about change and are ignored by the test statistic.
- **Discordant pairs ($b$ and $c$):** Subjects who changed state. The test focuses exclusively on whether the direction of change favors $b$ over $c$ or vice versa.

## Hypotheses & Test Statistic

- **Null Hypothesis ($H_0$):** The marginal probabilities are equal ($p_b = p_c$). Changes in either direction occur with equal probability (marginal homogeneity).
- **Alternative Hypothesis ($H_1$):** $p_b \neq p_c$. There is a directional shift in outcomes.

### Formula

Under $H_0$, the statistic follows a [[Chi-Square distribution]] with 1 [[Degrees of Freedom|degree of freedom]] ($\text{df} = 1$):

$$\chi^2 = \frac{(b - c)^2}{b + c}$$

For small sample sizes where $b + c < 25$, Edwards' continuity correction is applied:

$$\chi^2_{\text{corrected}} = \frac{(\vert{}b - c\vert{} - 1)^2}{b + c}$$

## Concrete Example: Classifier Comparison

Suppose you train two [[Computer Vision Concepts|Computer Vision]] classifiers on the same set of 1,000 test images:

| Model                 | **Model B Correct** | **Model B Incorrect** |
| --------------------- | ------------------- | --------------------- |
| **Model A Correct**   | 800                 | **40** ($b$)          |
| **Model A Incorrect** | **10** ($c$)        | 150                   |

1. **Identify discordant pairs:** $b = 40$ (A right, B wrong), $c = 10$ (A wrong, B right).
2. **Calculate test statistic:**
$$\chi^2 = \frac{(40 - 10)^2}{40 + 10} = \frac{30^2}{50} = \frac{900}{50} = 18.0$$

3. **P-value assessment:** For $\text{df} = 1$, a $\chi^2$ score of $18.0$ yields $p < 0.0001$. We reject $H_0$ and conclude Model A significantly outperforms Model B.

When several classifiers are screened together, place McNemar as the pairwise post hoc after [[Cochran’s Q Test]], with multiplicity control: see [[Model Selection#Comparing Many Models|Model Selection]].