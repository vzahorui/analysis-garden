---
tags:
  - linear-algebra
---
A **matrix** is a two-dimensional grid of real numbers arranged in rows and columns, denoted by boldface upper-case letters (e.g., $\mathbf{A}, \mathbf{B}, \mathbf{X}$).

The space of all continuous real-valued matrices with $m$ rows and $n$ columns is denoted by $\mathbb{R}^{m \times n}$. To express that a matrix $\mathbf{A}$ has dimensions $m \times n$, we use set membership:

$$\mathbf{A} \in \mathbb{R}^{m \times n}$$
Explicitly, an $m \times n$ matrix is written as:

$$\mathbf{A} = \begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \\ a_{21} & a_{22} & \dots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \dots & a_{mn} \end{bmatrix}$$

where each element $a_{ij}$ is a scalar belonging to the real numbers ($a_{ij} \in \mathbb{R}$ for $i \in \{1, \dots, m\}$ and $j \in \{1, \dots, n\}$).

A matrix can be viewed as a collection of [[Vector|vectors]] (either column or row vectors). 

### Key Notational Aspects

- **Element Indexing:** The entry in the $i$-th row and $j$-th column of matrix $\mathbf{A}$ is denoted by an italicized lower-case scalar $a_{ij}$, or using bracket notation $[\mathbf{A}]_{i,j}$.
- **Rows and Columns as Vectors:**
    - The $i$-th row can be represented as a row vector $\mathbf{a}_{i,:}^T \in \mathbb{R}^{1 \times n}$.
    - The $j$-th column can be represented as a column vector $\mathbf{a}_{:,j} \in \mathbb{R}^{m}$.
- **Transposition:** Transposing a matrix flips it over its main diagonal, swapping its rows and columns. If $\mathbf{A} \in \mathbb{R}^{m \times n}$, then its transpose $\mathbf{A}^T \in \mathbb{R}^{n \times m}$, where $[\mathbf{A}^T]_{ij} = a_{ji}$.
- **Discrete Matrix Domains:** If all entries of an $m \times n$ matrix are restricted to discrete values (e.g., binary elements), we apply the dimensions to the set:
$$\mathbf{A} \in \{0, 1\}^{m \times n}$$
