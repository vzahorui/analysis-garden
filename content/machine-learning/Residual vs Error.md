---
tags:
  - statistics
  - ML
aliases:
  - residual
  - error
  - noise
---
## Statistical Error ($\epsilon$)

- **Theoretical:** The difference between an observed value and the unobservable **true population value**.
- **Nature:** Represents inherent **noise** or irreducible uncertainty in data ($\epsilon \sim \mathcal{N}(0, \sigma^2)$).

## Residual ($e$)

- **Empirical:** The difference between an observed value ($y$) and the model's **predicted value** ($\hat{y}$).
- **Nature:** An observable quantity calculated directly from sample data ($e_i = y_i - \hat{y}_i$).
- Used in residual analysis to check model assumptions (e.g., homoscedasticity, normality).
