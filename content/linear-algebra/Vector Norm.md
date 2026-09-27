---
tags:
  - linear-algebra
aliases:
  - norm
---
A **vector norm** is a mathematical function that assigns a strictly positive length or size to a vector in a vector space. Formally, a norm maps a [[vector]] $\mathbf{x} \in \mathbb{R}^n$ to a non-negative real number $\Vert{}\mathbf{x}\Vert{}$.

In optimization, norms quantify two distinct things:

1. **Error / Distance:** Difference between target vector $\mathbf{y}$ and prediction vector $\mathbf{\hat{y}}$ ($\mathbf{e} = \mathbf{y} - \mathbf{\hat{y}}$). See [[Loss vs Metric|loss]].
2. **Complexity / Penalty:** Magnitude of the model parameter vector $\mathbf{w}$. See [[Regularization]].

## Formal Properties of a Norm

To be considered a valid norm, a function $\Vert{}\mathbf{x}\Vert{}$ must satisfy four axioms for all vectors $\mathbf{x}, \mathbf{y}$ and any scalar $c$:

1. **Non-negativity:** $\Vert{}\mathbf{x}\Vert{} \ge 0$
2. **Definiteness:** $\Vert{}\mathbf{x}\Vert{} = 0 \iff \mathbf{x} = \mathbf{0}$
3. **Absolute Homogeneity:** $\Vert{}c\mathbf{x}\Vert{} = \vert{}c\vert{} \Vert{}\mathbf{x}\Vert{}$
4. **Triangle Inequality:** $\Vert{}\mathbf{x} + \mathbf{y}\Vert{} \le \Vert{}\mathbf{x}\Vert{} + \Vert{}\mathbf{y}\Vert{}$

## Common Vector Norms

### $L_1$ Norm (Manhattan / Taxicab Norm)

Sum of the absolute values of the vector components.

$$\Vert{}\mathbf{x}\Vert{}_1 = \sum_{i=1}^{n} \vert{}x_i\vert{} = \vert{}x_1\vert{} + \vert{}x_2\vert{} + \dots + \vert{}x_n\vert{}$$

- **Intuition:** Distance traveled along a grid (like walking along city blocks).
- **Machine Learning Use:** 
    - $L_1$ [[regularization]] (Lasso) promotes sparsity by driving uninformative feature weights strictly to zero.
    - [[Mean Absolute Error]] loss function.

### 2. $L_2$ Norm (Euclidean Norm)

The standard straight-line distance from the origin to the vector endpoint.

$$\Vert{}\mathbf{x}\Vert{}_2 = \sqrt{\sum_{i=1}^{n} x_i^2} = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}$$

- **Intuition:** The shortest distance between two points in Euclidean space (Pythagorean theorem).
- **Machine Learning Use:** 
    - $L_2$ regularization (Ridge) penalizes large weights evenly across features without forcing them to exact zeros.
    - [[Mean Squared Error]] loss function.

### 3. $L_\infty$ Norm (Max / Chebyshev Norm)

The maximum absolute value among all components in the vector.

$$\Vert{}\mathbf{x}\Vert{}_\infty = \max_{1 \le i \le n} \vert{}x_i\vert{}$$

- **Intuition:** The largest single dimension displacement.

### 4. General $L_p$ Norm

The generalized family of norms for any real number $p \ge 1$:

$$\Vert{}\mathbf{x}\Vert{}_p = \left( \sum_{i=1}^{n} \vert{}x_i\vert{}^p \right)^{1/p}$$

## Summary Comparison

| **Norm**       | **Formula**              | **Geometric Shape (Unit Sphere ∥x∥=1)** | **Key Application**                   |
| -------------- | ------------------------ | --------------------------------------- | ------------------------------------- |
| **$L_1$**      | $\sum \Vert{}x_i\Vert{}$ | Diamond / Octahedron                    | Feature selection, sparse models      |
| **$L_2$**      | $\sqrt{\sum x_i^2}$      | Circle / Sphere                         | Gradient descent, distance metrics    |
| **$L_\infty$** | $\max \Vert{}x_i\Vert{}$ | Square / Cube                           | Error bounds, constraint optimization |

* $|x| + |y| \leq 1$ is a diamond: a square rotated $45^\circ$, with vertices on the axes at $\pm 1$.
* $x^2 + y^2 \leq 1$ is the disk whose outline is the unit circle.
* $\max(|x|, |y|) \leq 1$ is the square aligned with the axes, running from $-1$ to $1$ in both $x$ and $y$. Its corners $(\pm 1, \pm 1)$ lie outside the circle.

![[Vector Norm-1790417431279.webp]]