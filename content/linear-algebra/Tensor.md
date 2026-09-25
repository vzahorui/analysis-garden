---
tags:
  - linear-algebra
---
A **tensor** is a multi-dimensional array of real numbers, generalizing [[Scalar|scalars]] ($0$-order tensors), [[Vector|vectors]] ($1\text{st}$-order tensors), and [[Matrix|matrices]] ($2\text{nd}$-order tensors) to arbitrary dimensions. Tensors are typically denoted by boldface calligraphic or sans-serif upper-case letters (e.g., $\mathbf{\mathcal{X}}, \mathbf{\mathcal{Y}}, \mathbf{\mathcal{A}}$).

The space of all continuous real-valued $k$-th order tensors with dimensions $d_1 \times d_2 \times \dots \times d_k$ is denoted by $\mathbb{R}^{d_1 \times d_2 \times \dots \times d_k}$. To express that a tensor $\mathbf{\mathcal{X}}$ has order $k$ and shape $(d_1, d_2, \dots, d_k)$, we use set membership:

$$\mathbf{\mathcal{X}} \in \mathbb{R}^{d_1 \times d_2 \times \dots \times d_k}$$

The order (also called the number of **axes**, **modes**, or **ranks**) defines the number of indices needed to locate a single element.

## Examples

With regards to [[Computer Vision Concepts|Computer Vision]] the 3rd-order tensors represent images which have height, width and channel (red, green or blue).

A dataset may represent a 4th-order tensor if distinct images are stacked along the first axis.
### Key Notational Aspects
- **Element Indexing:** An individual element of a tensor $\mathbf{\mathcal{X}}$ located at position $(i_1, i_2, \dots, i_k)$ is denoted by an italicized lower-case scalar:

$$x_{i_1, i_2, \dots, i_k} \in \mathbb{R}$$
where $i_j \in \{1, 2, \dots, d_j\}$ for each axis $j \in \{1, 2, \dots, k\}$.

- **Slices and Fiber Notations:**
    - **Fiber:** A 1D slice obtained by fixing all indices except one (e.g., $\mathbf{\mathcal{X}}_{:, j, k}$ is a vector along axis 1).
    - **Slice:** A 2D section obtained by fixing all indices except two (e.g., $\mathbf{\mathcal{X}}_{i, :, :}$ is a matrix slice).