---
tags:
  - ML/classification
---
While the [[ROC Curve]]-[[AUC]] is the "industry standard," it can be dangerously misleading when your classes are heavily imbalanced.

## Why ROC-AUC Fails on Imbalanced Data

ROC-AUC uses the **False Positive Rate (FPR)** on its x-axis.

$$\text{FPR} = \frac{\text{False Positives}}{\text{Actual Negatives}}$$

If you have **1,000,000 negative cases** (the "hay") and only **10 positive cases** (the "needles"), a model could mistakenly flag 1,000 negatives as positives.

- Your **FPR** would be $1,000 / 1,000,000 = 0.1\%$. This looks amazing on an ROC curve!
- However, you now have 1,000 false alarms for only 10 real cases. Your **Precision** is terrible.

## The Components of PR-AUC

The PR curve plots two metrics that ignore the "True Negatives" (the overwhelming majority) and focus entirely on the "Positive" class:

- **Recall (Sensitivity):** Of all the needles in the haystack, how many did you find?
$$\text{Recall} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$$

- **Precision:** When you shouted "I found a needle!", how often were you actually right?

$$\text{Precision} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}$$

## The PR Curve and AUC

The PR-AUC (often called **Average Precision**) summarizes the curve that results from testing every possible probability threshold.

- **The Goal:** A perfect model sits in the **top-right corner** (Precision = 1.0, Recall = 1.0), meaning it found every needle and never sounded a false alarm.
- **The Baseline:** Unlike ROC (where the baseline is always 0.5), the baseline for PR-AUC is equal to the **fraction of positive samples** in your data. If only 1% of your data is positive, your baseline "random" PR-AUC is 0.01.