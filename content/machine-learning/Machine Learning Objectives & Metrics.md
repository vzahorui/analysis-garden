---
tags:
  - statistics
  - ML
---
## Core Distinctions
- [[Loss vs Metric vs Objective]] — Optimization focus vs. Human/Business evaluation.
- [[Residual vs Error]] — Sample residuals vs. Population theoretical errors.

## Core Concepts
- [[Loss Function]] — Per-instance penalty minimized during optimization.
- [[Evaluation Metric]] — Dataset-level performance measure for interpretability.
- [[Residual]] — Observed minus predicted ($y - \hat{y}$).
- [[Statistical Error]] — Observed minus true value ($y - \mu$).

## Functions & Metrics Catalog
### Regression
- [[Mean Squared Error (MSE)]] — Differentiable, sensitive to outliers.
- [[Mean Absolute Error (MAE)]] — Robust to outliers, non-differentiable at zero.
- [[Huber Loss]] — Hybrid of MSE and MAE.
- [[Root Mean Squared Error (RMSE)]] — Expressed in target variable units.

### Classification
- [[Cross-Entropy Loss]] — Measures distance between probability distributions.