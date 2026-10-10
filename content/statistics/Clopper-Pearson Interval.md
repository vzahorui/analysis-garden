---
tags:
  - statistics
aliases:
  - Clopper–Pearson
  - exact binomial CI
  - Clopper-Pearson CI
---
The **Clopper-Pearson interval** is an exact [[Confidence Interval]] for a binomial proportion based on inverting two-sided binomial tests (equivalently, Beta quantiles), not a [[Normal Distribution|normal]] approximation.

With $x$ successes in $n$ trials and confidence level $1-\alpha$, the bounds are (for $0 < x < n$):

$$
L = B^{-1}_{\alpha/2}(x,\, n-x+1), \qquad
U = B^{-1}_{1-\alpha/2}(x+1,\, n-x)
$$

where $B^{-1}_{q}(a,b)$ is the $q$-quantile of a $\mathrm{Beta}(a,b)$ distribution. Conventions: if $x = 0$ then $L = 0$; if $x = n$ then $U = 1$.

## When to Use It

- When you want guaranteed (conservative) coverage from the exact binomial model.
- Small $n$, or when an “exact” label is required for reporting.

Trade-off: intervals are often wider than needed; for routine [[Machine Learning Concepts|ML]] accuracy reporting, [[Wilson Score Interval]] is usually enough.

## Relation to Siblings

- [[Wald Interval]]: normal plug-in; fails at $\hat{p} \in \{0,1\}$.
- [[Wilson Score Interval]]: score-test inversion; typically better average coverage and shorter length than Clopper-Pearson.

## See Also

- [[Confidence Interval]]
- [[Wald Interval]]
- [[Wilson Score Interval]]
- [[Hypothesis Testing]]
