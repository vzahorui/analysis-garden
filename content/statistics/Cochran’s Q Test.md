---
tags:
  - statistics/test
---
**Cochran’s Q test** is a non-parametric [[Hypothesis Testing|statistical test]] used to determine if there are significant differences among **three or more matched or paired groups** when the outcome variable is **binary** (dichotomous—such as Success/Failure, Yes/No, or 1/0).

It can be thought of as an extension of [[McNemar's Test]] (which only handles 2 matched groups) or a non-parametric equivalent of a Repeated Measures [[ANOVA]] for binary data.

## Key Characteristics & Conditions

- **Dependent Variable:** Binary / Categorical with exactly two outcomes (coded as 1 or 0).
- **Independent Variable:** Categorical with $\ge 3$ related or matched groups (e.g., repeated measurements on the same subjects, or matched blocks of subjects).
- **Null Hypothesis ($H_0$):** The proportion of success is equal across all treatments/time points ($\pi_1 = \pi_2 = \dots = \pi_k$).
- **Alternative Hypothesis ($H_1$):** At least one treatment/time point has a significantly different proportion of success.

## When to Use It (Common Scenarios)

1. **Repeated Measures over Time:**
    
    Testing if the proportion of patients experiencing a symptom changes across three visits (Before Treatment, Week 2, Week 4) with responses recorded as `1` (Symptom Present) or `0` (Absent).
    
2. **Multiple Treatments / Diagnostic Tools:**
    
    Evaluating whether 3 different diagnostic tests produce different detection rates (`1` = Disease Detected, `0` = Not Detected) when applied to the exact same group of patients.
    
3. **Survey Rating Items:**
    
    Asking 50 users whether they like (`1`) or dislike (`0`) three different design prototypes.

4. Comparing performance of multiple [[Classification]] [[Machine Learning Concepts|Machine Learning]] models using binary [[Classification Metrics]]. For the screening → shortlist → Q → McNemar workflow, see [[Model Selection#Comparing Many Models|Model Selection]].

## How Cochran’s Q is Calculated

Given $k$ treatments/conditions evaluated across $N$ blocks/subjects:

- Let $x_{ij} \in \{0, 1\}$ be the response of subject $i$ to treatment $j$.
- $T_j = \sum_{i=1}^{N} x_{ij}$ is the column total (total number of successes for treatment $j$).
- $R_i = \sum_{j=1}^{k} x_{ij}$ is the row total (total number of successes for subject $i$).

The **Cochran’s $Q$ statistic** is calculated as:

$$Q = \frac{(k - 1) \left[ k \sum_{j=1}^{k} T_j^2 - \left(\sum_{j=1}^{k} T_j\right)^2 \right]}{k \sum_{i=1}^{N} R_i - \sum_{i=1}^{N} R_i^2}$$

### Test Distribution

Under the null hypothesis, $Q$ follows an approximate [[Chi-Square Distribution]] with **$\text{df} = k - 1$** [[degrees of freedom]]. If the calculated $Q$ yields a $p$-value less than your chosen significance level ($\alpha = 0.05$), you reject $H_0$.

## Practical Example

Imagine 5 users test 3 different user interface layouts (Layout A, Layout B, Layout C) to see if they can complete a task within 30 seconds (`1` = Success, `0` = Failure):

| **User ($i$)**     | **Layout A ($j$=1)** | **Layout B ($j$=2)** | **Layout C ($j$=3)** | **Row Total ($R_i​$)** | $R_i^2​$              |
| ------------------ | -------------------- | -------------------- | -------------------- | ---------------------- | --------------------- |
| **User 1**         | 1                    | 1                    | 0                    | **2**                  | 4                     |
| **User 2**         | 1                    | 0                    | 0                    | **1**                  | 1                     |
| **User 3**         | 1                    | 1                    | 1                    | **3**                  | 9                     |
| **User 4**         | 0                    | 0                    | 0                    | **0**                  | 0                     |
| **User 5**         | 1                    | 1                    | 0                    | **2**                  | 4                     |
| **Totals ($T_j$)** | **$T_1 = 4$**        | **$T_2 = 3$**        | **$T_3 = 1$**        | **$\sum R_i = 8$**     | **$\sum R_i^2 = 18$** |

### Step-by-Step Substitution:

- $k = 3$ (layouts), $N = 5$ (users)
- $\sum T_j = 4 + 3 + 1 = 8$
- $\sum T_j^2 = 4^2 + 3^2 + 1^2 = 16 + 9 + 1 = 26$

Substitute into the formula:

$$Q = \frac{(3 - 1) \left[ 3(26) - (8)^2 \right]}{3(8) - 18} = \frac{2 \left[ 78 - 64 \right]}{24 - 18} = \frac{2 \cdot 14}{6} = \frac{28}{6} \approx 4.67$$

### Conclusion

Compare $Q = 4.67$ against a Chi-Square table with $\text{df} = 3 - 1 = 2$. The critical value at $\alpha = 0.05$ with $2$ degrees of freedom is **$5.991$**. Since $4.67 < 5.991$, we **fail to reject $H_0$**—there is no statistically significant difference in success rates among the three layouts.

## Key Assumptions & What Comes Next

- **Independence across subjects:** The subjects/blocks must be independent of one another (though the measurements within a subject are matched/related).
- **Sample size:** Cochran's $Q$ relies on a chi-square approximation, so it performs best when $N \times k \ge 24$.
- **Post-hoc Analysis:** If $Q$ is significant, it tells you that _at least one_ treatment differs, but not _which_ ones. You perform post-hoc pairwise comparisons using [[McNemar's Test]] with a correction for multiple comparisons (like the [[Multiple Hypothesis Testing#Benjamini-Hochberg (BH) Procedure]]).