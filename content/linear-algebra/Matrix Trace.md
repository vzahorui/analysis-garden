---
tags:
  - linear-algebra
aliases:
  - trace
---
The **trace of a square matrix**—defined as the sum of its diagonal elements ($\text{Tr}(A) = \sum_{i=1}^n a_{ii}$)—is one of the most fundamental operations in [[Linear Algebra Concepts|Linear Algebra]]. Despite its simple definition, it acts as a bridge connecting linear transformations, geometry, statistics, and physical systems.

## Key Mathematical Properties

The power of the trace comes from two crucial properties:
1. **Invariance Under Cyclic Permutations:**
$$\text{Tr}(ABC) = \text{Tr}(BCA) = \text{Tr}(CAB)$$

_(Note: $\text{Tr}(ABC) \neq \text{Tr}(ACB)$ in general)._
2. **Similarity Invariance:**

If $P$ is an invertible matrix, then:

$$\text{Tr}(P^{-1} A P) = \text{Tr}(A)$$
Because [[Matrix Change of Basis|change of basis]] operations take the form $P^{-1} A P$, **the trace is an intrinsic property of a linear transformation**, independent of the coordinate system chosen to represent it.

3. **Sum of [[Eigenvectors and Eigenvalues|eigenvalues]]:**
For any square matrix $A$ with eigenvalues $\lambda_1, \lambda_2, \dots, \lambda_n$:
$$\text{Tr}(A) = \sum_{i=1}^n \lambda_i$$

## Major Uses & Applications

### Geometry & Vector Spaces

- **Matrix Inner Product ([[Frobenius Inner Product]]):**
The standard inner product on the space of matrices is defined using the trace:
$$\langle A, B \rangle = \text{Tr}(A^\top B)$$
- Calculation of [[Frobenius Norm]].

### [[Statististical Concepts|Statistics]] & [[Machine Learning Concepts|Machine Learning]]

- **Total Variance:** If $\Sigma$ is a covariance matrix, $\text{Tr}(\Sigma)$ equals the sum of the variances of all individual variables (the total variance of the dataset).
- **Derivatives of Matrix Expressions:** The trace trick is heavily used in multivariate statistics and  [[Deep Learning Concepts|Deep Learning]] [[Backpropagation]] to compute [[Derivative|derivatives]] of scalar functions involving matrices (e.g., $\nabla_X \text{Tr}(AXB)$).