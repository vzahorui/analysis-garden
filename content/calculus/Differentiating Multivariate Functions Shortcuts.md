---
tags:
  - linear-algebra
  - calculus
---
# Key Premise: [[Matrix]] [[Calculus Concepts|calculus]] & Gradient Convention

In multivariate calculus and deep learning, $\mathbf{x} \in \mathbb{R}^n$ is an $n \times 1$ column [[vector]]. The [[Derivative#Gradient]] operator $\nabla_{\mathbf{x}}$ collects all partial derivatives with respect to each element $x_i$ into a column vector:

$$\nabla_{\mathbf{x}} f(\mathbf{x}) = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{bmatrix}$$

## Linear Forms

$\nabla_{\mathbf{x}} (\mathbf{A}\mathbf{x}) = \mathbf{A}^\top$

- **Context:** $\mathbf{A}$ is an $m \times n$ matrix, so $\mathbf{A}\mathbf{x}$ is a vector in $\mathbb{R}^m$ (see [[Matrix Operations#Matrix-Vector Multiplication]]).
- **Meaning:** The [[derivative]] of a vector output with respect to a column vector input yields an $n \times m$ matrix (the transpose of the [[Jacobian]]).
- **Component-wise:** The $i$-th component of $\mathbf{A}\mathbf{x}$ is $y_i = \sum_{k=1}^n A_{ik} x_k$. The partial derivative $\frac{\partial y_i}{\partial x_j} = A_{ij}$. Assembling these across all entries gives $\mathbf{A}^\top$. Transposing happens here because the output of $\mathbf{A}\mathbf{x}$ is an $m \times 1$ vector, and when taking a gradient, we do it with respect ot each **output** component. 

$\nabla_{\mathbf{x}} (\mathbf{x}^\top \mathbf{A}) = \mathbf{A}$

- **Context:** Here, $\mathbf{x}^\top \mathbf{A}$ outputs a row vector in $\mathbb{R}^{1 \times n}$.
- **Meaning:** Taking the gradient with respect to $\mathbf{x}$ flips the dimensions back, yielding the $m \times n$ matrix $\mathbf{A}$.
## Quadratic Forms

$\nabla_{\mathbf{x}} (\mathbf{x}^\top \mathbf{A} \mathbf{x}) = (\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$

- **Context:** $\mathbf{A}$ is an $n \times n$ square matrix. The expression $f(\mathbf{x}) = \mathbf{x}^\top \mathbf{A} \mathbf{x}$ evaluates to a single [[scalar]] (a quadratic polynomial in the components of $\mathbf{x}$).
- **Intuition:** This is the vector equivalent of the single-variable power rule $\frac{d}{dx}(a x^2) = 2ax$.
- **Why the sum $(\mathbf{A} + \mathbf{A}^\top)$ appears:**
    Expanding $f(\mathbf{x}) = \sum_{i=1}^n \sum_{j=1}^n A_{ij} x_i x_j$ and taking the derivative with respect to $x_k$:
$$\frac{\partial f}{\partial x_k} = \sum_{j=1}^n A_{kj} x_j + \sum_{i=1}^n A_{ik} x_i$$
    The first sum corresponds to row $k$ of $\mathbf{A}$ multiplied by $\mathbf{x}$ (giving $\mathbf{A}\mathbf{x}$), and the second sum corresponds to column $k$ of $\mathbf{A}$ multiplied by $\mathbf{x}$ (giving $\mathbf{A}^\top \mathbf{x}$). Combining them gives $(\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$.
- **Symmetric Special Case:** If $\mathbf{A}$ is symmetric ($\mathbf{A} = \mathbf{A}^\top$), this simplifies directly to $2\mathbf{A}\mathbf{x}$.
## Vector Norm Squared

$\nabla_{\mathbf{x}} \Vert{}\mathbf{x}\Vert{}^2 = \nabla_{\mathbf{x}} (\mathbf{x}^\top \mathbf{x}) = 2\mathbf{x}$

- **Meaning:** The squared L2 norm is $\Vert{}\mathbf{x}\Vert{}^2 = x_1^2 + x_2^2 + \dots + x_n^2$.
- **Derivation:** This is a direct application of Rule 2 where $\mathbf{A} = \mathbf{I}$ (the identity matrix). Since $\mathbf{I} = \mathbf{I}^\top$, the derivative becomes $(\mathbf{I} + \mathbf{I}^\top)\mathbf{x} = 2\mathbf{x}$.
- **Component-wise:** $\frac{\partial}{\partial x_k}(x_1^2 + \dots + x_n^2) = 2x_k$. Stacking these partial derivatives for $k=1, \dots, n$ yields the vector $2\mathbf{x}$.
## Matrix Frobenius Norm Squared

$\nabla_{\mathbf{X}} \Vert{}\mathbf{X}\Vert{}_\textrm{F}^2 = 2\mathbf{X}$

- **Context:** $\mathbf{X}$ is a matrix of shape $m \times n$. The Frobenius norm squared is the sum of squares of every individual element in the matrix:
$$\Vert{}\mathbf{X}\Vert{}_\textrm{F}^2 = \sum_{i=1}^m \sum_{j=1}^n X_{ij}^2$$
- **Meaning:** $\nabla_{\mathbf{X}}$ asks for the partial derivative of this scalar sum with respect to every matrix entry $X_{ij}$.
- **Derivation:** The partial derivative with respect to entry $X_{ij}$ is simply $\frac{\partial}{\partial X_{ij}} (X_{ij}^2) = 2X_{ij}$. Since this holds for every position $(i, j)$, arranging these partial derivatives back into matrix shape yields $2\mathbf{X}$.