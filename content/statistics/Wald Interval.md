---
tags:
  - statistics
aliases:
  - Wald CI
  - Wald confidence interval
---
The **Wald interval** is the [[Normal Distribution|normal]]-approximation [[Confidence Interval]] for a binomial proportion $\hat{p} = x/n$ (e.g. accuracy as successes over evaluation rows).

Let $z = z_{1-\alpha/2}$ be the standard normal critical value (about $1.96$ for 95%). The Wald form centers on $\hat{p}$ and uses the plug-in [[Sampling Distribution|standard error]]:

$$\mathrm{SE}(\hat{p}) = \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}, \qquad
\hat{p} \pm z\,\mathrm{SE}(\hat{p})$$

## When to Use It

- Large $n$ and $\hat{p}$ comfortably away from $0$ and $1$.
- Quick planning formulas that rearrange $z\,\mathrm{SE} \approx E$ into a sample-size rule (as in [[Train and Test#Validation Size and Confidence Intervals]]).

## Failure Modes

- When $\hat{p} = 0$ or $\hat{p} = 1$, $\mathrm{SE} = 0$ and the interval collapses to a point even though uncertainty remains.
- Near the boundaries, or with small $n$, coverage is often below the nominal level, and bounds can fall outside $[0, 1]$.

Prefer [[Wilson Score Interval]] for reporting in those regimes, or [[Clopper-Pearson Interval]] when you want an exact binomial inversion.

## See Also

- [[Confidence Interval]]
- [[Wilson Score Interval]]
- [[Clopper-Pearson Interval]]
- [[Bernoulli Trial]]
