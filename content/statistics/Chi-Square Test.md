---
tags:
  - statistics/test
---
A **Chi-Square ($\chi^2$) Test** is a non-parametric statistical [[Hypothesis Testing|hypothesis test]] used to analyze categorical data. It evaluates whether the discrepancies between observed counts and expected counts are due to random chance or represent a statistically significant pattern.

## Core Mathematical Formula

The Chi-Square test statistic measures overall divergence across $k$ categories or cells. Its statistic comes from [[Chi-Square Distribution]]:

$$\chi^2 = \sum_{i=1}^{k} \frac{(O_i - E_i)^2}{E_i}$$

- **$O_i$**: Observed frequency (actual count in sample data).
- **$E_i$**: Expected frequency (theoretical count under the null hypothesis).
- **$(O_i - E_i)^2$**: Squaring prevents positive and negative differences from canceling out and gives heavier weight to larger deviations.
- **Dividing by $E_i$**: Normalizes the squared deviation relative to the expected scale.

## The Two Main Types of Chi-Square Tests

### A. Chi-Square Goodness-of-Fit Test

Evaluates whether a single categorical variable follows a specified theoretical distribution.

- **Null Hypothesis ($H_0$)**: The observed frequency distribution matches the expected distribution.
- [[Degrees of Freedom]]: $df = k - 1$, where $k$ is the number of categories.
- **Example**: Testing if a six-sided die is fair. In 60 rolls, you expect each face to land 10 times ($E_i = 10$). If face "6" appears 25 times, the goodness-of-fit test quantifies whether that skew is random noise or bias.

### B. Chi-Square Test of Independence

Evaluates whether two categorical variables are statistically independent or associated with each other using a contingency table ($r$ rows $\times$ $c$ columns).

- **Null Hypothesis ($H_0$)**: Variable A and Variable B are independent (no relationship).
- **Expected Frequency Formula**: For each cell at row $i$ and column $j$:
$$E_{i,j} = \frac{\text{Row } i \text{ Total} \times \text{Column } j \text{ Total}}{\text{Total Sample Size } (N)}$$
- **Degrees of Freedom ($df$)**: $df = (r - 1) \times (c - 1)$.
- **Example**: Testing whether customer device preference (iOS vs. Android) depends on age group (Under 30, 30–50, Over 50).

## Worked Step-by-Step Example

Suppose you survey 100 students to see if preferred learning mode (Visual vs. Auditory) differs by major (STEM vs. Arts).

### Observed Counts ($O$)

|**Major**|**Visual**|**Auditory**|**Row Total**|
|---|---|---|---|
|**STEM**|40|10|**50**|
|**Arts**|20|30|**50**|
|**Column Total**|**60**|**40**|**$N = 100$**|

### Step 1: Calculate Expected Counts ($E$) under $H_0$

- $E_{\text{STEM, Visual}} = \frac{50 \times 60}{100} = 30$

- $E_{\text{STEM, Auditory}} = \frac{50 \times 40}{100} = 20$

- $E_{\text{Arts, Visual}} = \frac{50 \times 60}{100} = 30$

- $E_{\text{Arts, Auditory}} = \frac{50 \times 40}{100} = 20$

### Step 2: Compute $\chi^2$ Component for Each Cell

$$\chi^2 = \frac{(40 - 30)^2}{30} + \frac{(10 - 20)^2}{20} + \frac{(20 - 30)^2}{30} + \frac{(30 - 20)^2}{20}$$

$$\chi^2 = \frac{100}{30} + \frac{100}{20} + \frac{100}{30} + \frac{100}{20} = 3.33 + 5.00 + 3.33 + 5.00 = 16.66$$

### Step 3: Evaluate Significance

- **Degrees of Freedom**: $df = (2 - 1) \times (2 - 1) = 1$.
- **Critical Value ($\alpha = 0.05, df = 1$)**: $3.841$.
- **Conclusion**: Since $\chi^2 = 16.66 > 3.841$ (or $p < 0.001$), reject $H_0$. Preferred learning mode and major are significantly associated.

## Key Assumptions & Constraints

1. **Categorical Data**: Counts or frequencies of mutually exclusive categories (not continuous measurements or percentages).
2. **Independence of Observations**: Each individual or event contributes to exactly one cell in the table.
3. **Minimum Expected Cell Count**: The standard rule of thumb requires $E_i \ge 5$ in at least 80% of cells (and no $E_i = 0$). For small sample sizes where this fails, **Fisher's Exact Test** is used instead.