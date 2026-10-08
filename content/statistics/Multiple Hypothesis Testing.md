---
tags:
  - statistics
  - statistics/test
---
When testing a single [[Hypothesis Testing|hypothesis]] at a significance level of $\alpha = 0.05$, there is a 5% chance of committing a **Type I error** (a false positive—rejecting a true null hypothesis).

However, when you test **multiple hypotheses simultaneously** (such as evaluating thousands of genes in a genomic study, testing dozens of features in A/B testing, or checking spatial statistical metrics across multiple regions), the probability of finding at least one false positive increases exponentially.

## The Multiple Testing Problem

If you perform $m$ independent hypothesis tests, each at significance level $\alpha$:

$$\text{Probability of NO false positive in 1 test} = 1 - \alpha$$

$$\text{Probability of NO false positives in } m \text{ tests} = (1 - \alpha)^m$$

$$\text{Family-Wise Error Rate (FWER)} = 1 - (1 - \alpha)^m$$

### Cumulative False Positive Rate

|**Number of Tests (m)**|**Chance of ≥1 False Positive (α=0.05)**|
|---|---|
|1|5.0%|
|5|22.6%|
|20|64.2%|
|100|99.4%|

By the time you run 20 tests, you are more likely than not to obtain a statistically significant result purely due to random chance.

To prevent false discoveries from driving decisions, you must adjust either the individual significance thresholds or the $p$-values themselves. The two main frameworks for controlling false positives are **Family-Wise Error Rate (FWER)** and **False Discovery Rate (FDR)**.

## Family-Wise Error Rate (FWER) & The Bonferroni Correction

**FWER** is the probability of making **at least one** Type I error across the entire family of $m$ tests:

$$\text{FWER} = P(V \ge 1) \le \alpha$$

where $V$ is the number of false positives.

### Bonferroni Correction

The Bonferroni correction is the simplest and most conservative method to control the FWER. To maintain an overall significance level of $\alpha$ across $m$ tests, you adjust the single-test threshold $\alpha_{\text{adjusted}}$:

$$\alpha_{\text{adjusted}} = \frac{\alpha}{m}$$

#### Strengths & Limitations

- **Pros:** Extremely simple to compute; makes no assumptions about independence among tests.
- **Cons:** Highly conservative. As $m$ grows large (e.g., thousands of tests), the threshold becomes minuscule, severely inflating Type II errors (false negatives) and destroying statistical power.

## False Discovery Rate (FDR) & The Benjamini-Hochberg Procedure

In large-scale exploratory data science or screening experiments, controlling FWER is often overly strict. Expecting zero false positives out of 10,000 tests is impractical.

Instead, **False Discovery Rate (FDR)** controls the **expected proportion of false positives among all rejected hypotheses (discoveries)**:

$$\text{FDR} = E \left[ \frac{V}{R} \right] = E \left[ \frac{\text{False Positives}}{\text{Total Significant Results}} \right]$$

_(where $\frac{V}{R} = 0$ if $R = 0$)_

Setting an FDR target of $q = 0.05$ means that among all the hypotheses you declare significant, you accept that on average ~5% of them may be false positives.

```
                  Null True (H0)   Null False (H1)    Total
Declaring Sig.          V                 S             R (Total Discoveries)
Not Sig.                U                 T            m - R
Total                   m0               m - m0          m
```

### Benjamini-Hochberg (BH) Procedure

The Benjamini-Hochberg procedure controls the FDR at target rate $q$ (e.g., $q = 0.05$) using the following steps:

1. **Sort:** Rank all $m$ raw $p$-values in ascending order: $p_{(1)} \le p_{(2)} \le \dots \le p_{(m)}$.
2. **Calculate Thresholds:** For each rank $i$, calculate a dynamic critical value:

$$Q_i = \left( \frac{i}{m} \right) \cdot q$$

3. **Find Cutoff:** Find the largest rank $k$ such that:

$$p_{(k)} \le \left( \frac{k}{m} \right) \cdot q$$

4. **Reject:** Declare all hypotheses corresponding to $p_{(1)}, p_{(2)}, \dots, p_{(k)}$ as statistically significant.

## Comparison of Methods

| **Method**               | **Metric Controlled**         | **Target Error Standard**                                    | **Statistical Power** | **Best Use Case**                                                                       |
| ------------------------ | ----------------------------- | ------------------------------------------------------------ | --------------------- | --------------------------------------------------------------------------------------- |
| **Unadjusted $p$-value** | Per-comparison error rate     | $P(\text{False Positive}) \le \alpha$ per test               | Highest               | Single pre-specified hypothesis                                                         |
| **Bonferroni**           | Family-Wise Error Rate (FWER) | $P(\ge 1 \text{ False Positive}) \le \alpha$                 | Lowest                | Small number of critical tests ($m < 20$) where false positives carry high cost         |
| **Benjamini-Hochberg**   | False Discovery Rate (FDR)    | $E[\text{False Positives} / \text{Total Discoveries}] \le q$ | High                  | High-dimensional data, genomics, [[AB Testing]] multiple metrics, exploratory screening |

## Practical Worked Example

Suppose you run $m = 5$ tests at a target error level of $0.05$ (so $\alpha = 0.05$ and target $q = 0.05$).

**Raw $p$-values:** `[0.003, 0.012, 0.018, 0.035, 0.120]`

### 1. Unadjusted

Threshold is $\alpha = 0.05$.

- Tests with $p < 0.05$ rejected: **4 significant results** (`0.003`, `0.012`, `0.018`, `0.035`).

### 2. Bonferroni Correction

Threshold is $\alpha / m = 0.05 / 5 = 0.010$.

- Only $p = 0.003 \le 0.010$: **1 significant result** (`0.003`).

### 3. Benjamini-Hochberg (FDR = 0.05)

Rank p-values and evaluate $p_{(i)} \le \frac{i}{5} \times 0.05$:

|**Rank (i)**|**Raw p(i)​**|**BH Threshold (5i​×0.05)**|**p(i)​≤Threshold?**|
|---|---|---|---|
|1|0.003|0.010|Yes|
|2|0.012|0.020|Yes|
|3|0.018|0.030|**Yes** ($k=3$)|
|4|0.035|0.040|No|
|5|0.120|0.050|No|

- The largest rank meeting the condition is $k = 3$ ($p_{(3)} = 0.018 \le 0.030$).
- Reject $p_{(1)}, p_{(2)}, p_{(3)}$: **3 significant results** (`0.003`, `0.012`, `0.018`).