---
tags:
  - ML/classification
---
The **AUC** measures the entire two-dimensional area underneath the entire [[ROC Curve]] curve. It provides an aggregate measure of performance across all possible classification thresholds.

- **AUC = 1.0:** A perfect model. It can perfectly separate the two classes without any overlap.
- **AUC = 0.5:** A useless model. This is equivalent to random guessing (a diagonal line from bottom-left to top-right).
- **AUC = 0.7 to 0.9:** Generally considered a good, functional model.

### The "Probabilistic" Interpretation

One of the most intuitive ways to think about AUC is this:

> If you pick one random positive instance and one random negative instance, the AUC is the probability that your model will rank the positive instance higher than the negative one.