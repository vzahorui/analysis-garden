---
tags:
  - linear-algebra
---
# Matrix-Vector Multiplication

Multiplies an $m \times n$ [[matrix]] $A$ by an $n \times 1$ column [[vector]] $x$ to yield an $m \times 1$ column vector $y$:
$$\mathbf{y} = \mathbf{A} \mathbf{x}$$
Each element $y_i$ is computed as the [[Vector Operations#Dot Product (Inner Product)]] of the $i$-th row vector of $\mathbf{A}$ and the vector $\mathbf{x}$:
$$y_i = \sum_{j=1}^{n} A_{ij} x_j$$
**Used in**:
- **Linear Transformation:** Geometrically, $\mathbf{A} \mathbf{x}$ maps a vector $\mathbf{x}$ from an $n$-dimensional space to an $m$-dimensional space.
- **ML Application (Linear Layer Forward Pass):** In a dense [[neural network]] layer, $\mathbf{y} = \mathbf{W} \mathbf{x} + \mathbf{b}$, where $\mathbf{W}$ is the weight matrix, $\mathbf{x}$ is the input feature vector, and $\mathbf{b}$ is the bias vector.

# Matrix-Matrix Multiplication

Multiplies an $m \times n$ matrix $\mathbf{A}$ by an $n \times p$ matrix $\mathbf{B}$ to produce an $m \times p$ matrix $\mathbf{C}$:
$$\mathbf{C} = \mathbf{A} \mathbf{B}$$
Each element $C_{ij}$ is the dot product of the $i$-th row vector of $\mathbf{A}$ and the $j$-th column of $\mathbf{B}$:
$$C_{ij} = \sum_{k=1}^{n} A_{ik} B_{kj}$$
It's a generalization of Matrix-Vector Multiplication in which the actual operation is repeated for each column vector of $\mathbf{B}$, and thus the result is a set of column vectors, which in turn are put into a new matrix.

**Used by:
- **Batch Processing:** Instead of passing one sample vector $\mathbf{x}$ through a neural network, a batch of $m$ samples stacked as rows in matrix $\mathbf{X}$ ($m \times n$) is transformed in parallel using $\mathbf{X W}$ ($m \times p$).
- **Computational Engine:** General Matrix Multiply (GEMM) is the primary target optimized by modern hardware acceleration units (such as Nvidia Tensor Cores or Apple Neural Engine).

# Element-Wise Multiplication 

See [[Hadamard Product]].

# Matrix Transposition

Transposing an $m \times n$ matrix $\mathbf{A}$, written as $\mathbf{A}^T$, swaps its rows and columns to yield an $n \times m$ matrix where $(A^T)_{ij} = A_{ji}$.

**Used by**:
- **[[Gradient Descent| Gradient Computation]] (Backpropagation):** Given a linear loss gradient $\frac{\partial L}{\partial Y}$ of dimension $m \times p$ and inputs $X$ ($m \times n$), the weight gradient is computed using transpositions:
$$\frac{\partial L}{\partial W} = X^T \left(\frac{\partial L}{\partial Y}\right)$$
- **[[Covariance]] and Similarity:** $X^T X$ computes feature-wise scatter or covariance structures.

# Other References
* [[Frobenius Norm]]
* [[Frobenius Inner Product]]