---
tags:
  - linear-algebra
---

The **Frobenius norm** (also called the Hilbert–Schmidt norm) is the matrix equivalent of the standard Euclidean norm ($L_2$ norm) for vectors. It measures the "magnitude" or size of a matrix by taking the square root of the sum of the absolute squares of all its elements:

$$\Vert{}A\Vert{}_F = \sqrt{\sum_{i=1}^m \sum_{j=1}^n \vert{}a_{ij}\vert{}^2} = \sqrt{\text{Tr}(A^T A)}$$
## Matrix Weight [[Regularization]] ($L_2$ Regularization)

When regularizing fully connected layers, [[Linear Models]], or convolutional filter matrices, the weight decay penalty added to the loss function uses the squared Frobenius norm:

$$\mathcal{L}_{\text{total}} = \mathcal{L}_{\text{data}} + \frac{\lambda}{2} \Vert{}W\Vert{}_F^2$$

- **Purpose:** Keeps weight values small to prevent overfitting, improve generalization, and smooth the model's decision boundaries.
- **Why Frobenius?** Because it is strictly convex, everywhere differentiable, and computationally efficient to compute alongside standard backpropagation gradients.