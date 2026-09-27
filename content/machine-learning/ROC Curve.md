---
tags:
  - ML/classification
aliases:
  - ROC
---
The **Receiver Operating Characteristic** curve is a graph that shows the performance of a classification model at all possible classification thresholds.

Most models don't just output "Yes" or "No"; they output a probability (like $0.85$). To make a decision, you choose a **threshold**. If you set it at $0.5$, everything above is "Positive." If you move it to $0.9$, you become much more conservative.

The curve plots two parameters:

- **True Positive Rate (TPR) / Sensitivity:** Of all actual positives, how many did we catch?

$$\text{TPR} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$$

- **False Positive Rate (FPR):** Of all actual negatives, how many did we "falsely" flag as positive?

$$\text{FPR} = \frac{\text{False Positives}}{\text{False Positives} + \text{True Negatives}}$$

![[ROC-1790528551971.webp]]

As you lower the threshold, you catch more positives (TPR goes up), but you also start catching more "false" positives (FPR goes up). The ROC curve traces this trade-off.

## The **Youden Point** 

The **Youden Point** (also known as **Youden’s $J$ statistic**) on a Receiver Operating Characteristic (ROC) curve is the point that maximizes the trade-off between **Sensitivity** (True Positive Rate) and **Specificity** (True Negative Rate).

It identifies the single optimal decision threshold for a binary classifier when you treat false positives and false negatives as equally costly.

### Mathematical Definition

Youden’s index $J$ for a given cutoff threshold $c$ is defined as:

$$J(c) = \text{Sensitivity}(c) + \text{Specificity}(c) - 1$$

Alternatively, since $\text{Specificity} = 1 - \text{False Positive Rate (FPR)}$, it can be written using ROC axes:

$$J(c) = \text{True Positive Rate (TPR)} - \text{False Positive Rate (FPR)}$$

- **Range:** $J$ ranges from **0 to 1** (or -1 to 1 in non-informative classifiers).
    
    - $J = 1$: Perfect test with no false positives or false negatives.
        
    - $J = 0$: Test with no predictive value (equivalent to a random guess along the diagonal chance line).
        

The **Youden Point** is the specific operating threshold $c^*$ that maximizes $J$:

$$c^* = \arg\max_c J(c)$$
### Key Properties & Assumptions

- **Equal Cost Weighting:** Youden's $J$ assumes that a **False Positive** costs the exact same as a **False Negative**.
    
- **Equal Class Prevalence:** It assumes the base prevalence of positive and negative classes is balanced ($50/50$) or equally important to detect.
    
- **Prevalence Sensitivity:** Unlike metrics like Precision or F1-Score, Youden's index is invariant to changes in population prevalence because Sensitivity and Specificity are rates calculated within true condition states.
    

### When Should You Use (or Avoid) It?

- **Use when:** You need an objective, unweighted criterion to select a single continuous threshold (e.g., setting a diagnostic cutoff for a blood biomarker) and have no prior reason to penalize one type of error over another.
    
- **Avoid when:** Costs are asymmetric. For example, in screening for a fatal disease, a False Negative (missing a sick patient) is far worse than a False Positive (a follow-up test). In such cases, you should adjust the threshold using a cost-benefit matrix or custom loss function instead of the standard Youden point.