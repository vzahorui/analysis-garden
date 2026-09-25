---
tags:
  - calculus
  - linear-algebra
---
The **Jacobian [[matrix]]** is the multi-variable equivalent of a single-variable [[derivative]]. It collects all first-order partial derivatives of a vector-valued function, representing the best linear approximation of that function near a specific point.

It is the direct generalization of the [[Derivative|gradient]] to functions with multiple outputs.

## Mathematical Definition

Consider a function $\mathbf{f}: \mathbb{R}^n \to \mathbb{R}^m$ that takes a vector of $n$ inputs $\mathbf{x} = (x_1, x_2, \dots, x_n)$ and outputs a vector of $m$ functions $\mathbf{f}(\mathbf{x}) = (f_1, f_2, \dots, f_m)$.

The Jacobian matrix $\mathbf{J}$ (or $D\mathbf{f}$) is an $m \times n$ matrix defined as:

$$\mathbf{J} = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \frac{\partial f_m}{\partial x_2} & \cdots & \frac{\partial f_m}{\partial x_n} \end{bmatrix}$$

- **Rows ($m$):** Correspond to each output component $f_i$.
- **Columns ($n$):** Correspond to partial derivatives with respect to each input variable $x_j$.

Using the Jacobian, a local change in output $\Delta \mathbf{f}$ due to a small change in input $\Delta \mathbf{x}$ is approximated via matrix multiplication:

$$\Delta \mathbf{f} \approx \mathbf{J} \Delta \mathbf{x}$$
