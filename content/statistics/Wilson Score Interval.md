---
tags:
  - statistics
aliases:
  - Wilson interval
  - Wilson CI
  - score interval
---
The **Wilson score interval** is a [[Confidence Interval]] for a binomial proportion $\hat{p} = x/n$ obtained by inverting the normal score test for $H_0: p = p_0$, rather than plugging $\hat{p}$ into a Wald SE.

Let $z = z_{1-\alpha/2}$. One closed form is:

$$\frac{\hat{p} + \dfrac{z^{2}}{2n} \pm z\sqrt{\dfrac{\hat{p}(1-\hat{p})}{n} + \dfrac{z^{2}}{4n^{2}}}}{1 + \dfrac{z^{2}}{n}}$$

The center is a shrunk version of $\hat{p}$ pulled toward $1/2$; the width stays positive even when $\hat{p} \in \{0, 1\}$, and the bounds stay inside $[0, 1]$.

## When to Use It

- Default choice for reporting a single proportion when $n$ is moderate or $\hat{p}$ is near $0$ or $1$.
- Same setting as the [[Wald Interval]], but with much better coverage in the regimes where Wald breaks.

## Relation to Siblings

- [[Wald Interval]]: simpler, worse near boundaries.
- [[Clopper-Pearson Interval]]: exact binomial inversion; often wider (more conservative).

## See Also

- [[Confidence Interval]]
- [[Wald Interval]]
- [[Clopper-Pearson Interval]]
