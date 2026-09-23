---
tags:
  - EDA
  - statistics
aliases:
  - correlation coefficient
  - Pearson
---
**Pearson correlation coefficient** (denoted as $r$ for a sample or $\rho$ for a population) measures the strength and direction of a **linear relationship** between two continuous variables.

It tells you how predictably one variable changes in a straight line relative to another.

## Key Properties

- **Range:** Always between **$-1.0$** and **$+1.0$**.
    - **$+1.0$ (Perfect Positive Correlation):** As variable $X$ increases, variable $Y$ increases at a perfectly constant rate.
    - **$0.0$ (No Linear Correlation):** No straight-line relationship exists between $X$ and $Y$.
    - **$-1.0$ (Perfect Negative Correlation):** As variable $X$ increases, variable $Y$ decreases at a perfectly constant rate.

## The Mathematical Formula

For two variables $X$ and $Y$, the sample Pearson correlation coefficient $r$ is calculated as the [[covariance]] of $X$ and $Y$ divided by the product of their standard deviations:

$$r = \frac{\sum (X_i - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum (X_i - \bar{X})^2 \sum (Y_i - \bar{Y})^2}}$$
Where:
- $X_i, Y_i$ are individual data points.
- $\bar{X}, \bar{Y}$ are the sample means of $X$ and $Y$.
## Core Assumptions

Pearson correlation requires specific data conditions to produce valid results:
1. **Interval or Ratio Scale:** Both variables must be continuous quantitative measurements.
2. **Linearity:** The relationship between $X$ and $Y$ must be a straight line (check with a scatter plot).
3. [[Normality]]: Both variables should follow an approximately normal distribution.
4. **No Significant Outliers:** Outliers can drastically distort $r$ toward or away from zero.
5. **Homoscedasticity:** The variance of data points around the line of best fit should be roughly constant across all values of $X$.
## Critical Pitfalls & Caveats

- **Non-Linear Relationships:** Pearson correlation _only_ measures linear trends. A U-shaped curve (like quadratic data) can have a Pearson $r = 0$, even though a strong relationship exists.
- **Sensitivity to Outliers:** A single extreme data point can artificially inflate or flatten $r$.
- **Correlation $\neq$ Causation:** A high $r$ between ice cream sales and sunburns does not mean ice cream causes sunburns; both are driven by a third variable (temperature).
