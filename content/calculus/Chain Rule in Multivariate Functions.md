---
tags:
  - calculus
  - linear-algebra
---
# One Independent Variable (Single Parameter)

Suppose $z = f(x, y)$, where both $x$ and $y$ depend on a single variable $t$:

- $x = x(t)$
- $y = y(t)$

Here, $z$ ultimately depends only on $t$. To find the total [[derivative]] $\frac{dz}{dt}$:

$$\frac{dz}{dt} = \frac{\partial z}{\partial x} \frac{dx}{dt} + \frac{\partial z}{\partial y} \frac{dy}{dt}$$
# Multiple Independent Variables

Suppose $z = f(x, y)$, but now $x$ and $y$ depend on two independent variables, $u$ and $v$:
- $x = x(u, v)$
- $y = y(u, v)$

Because $z$ now depends on multiple independent inputs, we take **partial derivatives** of $z$ with respect to $u$ or $v$.

To see how $z$ changes when only $u$ changes:

$$\frac{\partial z}{\partial u} = \frac{\partial z}{\partial x} \frac{\partial x}{\partial u} + \frac{\partial z}{\partial y} \frac{\partial y}{\partial u}$$

To see how $z$ changes when only $v$ changes:

$$\frac{\partial z}{\partial v} = \frac{\partial z}{\partial x} \frac{\partial x}{\partial v} + \frac{\partial z}{\partial y} \frac{\partial y}{\partial v}$$
# The General Matrix Formulation (Jacobians)

In higher dimensions or vector calculus, writing out individual partial derivatives becomes tedious. [[Matrix]] notation unifies every case using **[[Jacobian]] matrices**.

If $\mathbf{x} \in \mathbb{R}^n$ and $\mathbf{f}: \mathbb{R}^n \to \mathbb{R}^m$, and $\mathbf{x} = \mathbf{g}(\mathbf{u})$ where $\mathbf{u} \in \mathbb{R}^k$, then the overall sensitivity of **final outputs** $\mathbf{y}$ to **inputs** $\mathbf{u}$ is this:

$$\mathbf{J}_{\mathbf{f} \circ \mathbf{g}}(\mathbf{u}) = \mathbf{J}_{\mathbf{f}}(\mathbf{g}(\mathbf{u})) \cdot \mathbf{J}_{\mathbf{g}}(\mathbf{u})$$
Notice how the matrix dimensions align for multiplication:
$$(m \times n) \cdot (n \times k) = (m \times k)$$

## Why Matrix Multiplication Works

Let's do that explicitly for entry $(i, j)$ of $\mathbf{J}_{\mathbf{f} \circ \mathbf{g}}$:
$$\text{Row } i \text{ of } \mathbf{J}_{\mathbf{f}}: \quad \begin{bmatrix} \frac{\partial f_i}{\partial x_1} & \frac{\partial f_i}{\partial x_2} & \cdots & \frac{\partial f_i}{\partial x_n} \end{bmatrix}$$
$$\text{Column } j \text{ of } \mathbf{J}_{\mathbf{g}}: \quad \begin{bmatrix} \frac{\partial x_1}{\partial u_j} \\ \frac{\partial x_2}{\partial u_j} \\ \vdots \\ \frac{\partial x_n}{\partial u_j} \end{bmatrix}$$
Multiplying row $i$ by column $j$ gives:

$$\frac{\partial f_i}{\partial u_j} = \frac{\partial f_i}{\partial x_1}\frac{\partial x_1}{\partial u_j} + \frac{\partial f_i}{\partial x_2}\frac{\partial x_2}{\partial u_j} + \dots + \frac{\partial f_i}{\partial x_n}\frac{\partial x_n}{\partial u_j} = \sum_{r=1}^{n} \frac{\partial f_i}{\partial x_r} \frac{\partial x_r}{\partial u_j}$$

This is the exact multivariate chain rule formula.