---
tags:
  - EDA
  - statistics
---
A **Q-Q plot** (Quantile-Quantile plot) is a scatterplot used to assess whether a dataset follows a specific theoretical [[Probability Distributions|distribution]] (most commonly a [[normal distribution]]) or whether two datasets come from the same distribution.

It is helpful when a downstream method assumes normality (for example, [[linear regression]]). We can use it to check before assuming.
## How It Works

1. **Sort your data:** Order the dataset values from smallest to largest.
2. **Calculate quantiles:** Divide the dataset into equal intervals (e.g., percentiles) so each point corresponds to a probability level.
3. **Generate theoretical quantiles:** Find the corresponding values at those same probability levels from a theoretical probability density function (like the standard normal distribution $N(0, 1)$).
4. **Plot the pairs:** Map the theoretical values on the **x-axis** and your empirical sample values on the **y-axis**. Add a $y = x$ reference line (or standard linear fit).

![[Q-Q Plot-1789921505831.webp]]

> [!Note]
> - $\Phi$ is the standard [[Normal Distribution|normal]] CDF: $\Phi(z)=P(Z≤z)$ for $Z∼N(0,1)$.
> -  $\Phi^{−1}$ is the quantile function (inverse CDF): the $z$ such that $\Phi(z)=p$.

## How to Read Deviations

The shape of the curve relative to the straight line tells you exactly how your data differs from the reference distribution:

| **Pattern on Q-Q Plot**                           | **Visual Curve Shape**                            | **Interpretation**                                                   |
| ------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------- |
| **Straight line**                                 | Points lie along the $45^\circ$ line              | Data matches the target distribution well.                           |
| **S-shape (Right curved at top, Left at bottom)** | Upward bend at high end, downward bend at low end | **Heavy tails:** Extreme values occur more frequently than expected. |
| **Inverted S-shape**                              | Downward curve at top, upward at bottom           | **Light tails:** Fewer extreme values than expected.                 |
| **Concave (U-shaped)**                            | Both ends curve upward                            | **Right-skewed:** Data has a long tail to the right.                 |
| **Convex (Inverted U)**                           | Both ends curve downward                          | **Left-skewed:** Data has a long tail to the left.                   |

![[Q-Q Plot-1789928932444.webp]]
## Watch for

Small samples produce noisy Q-Q plots. With N<30 expect scatter even from normal data.