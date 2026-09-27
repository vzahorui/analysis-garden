---
tags:
  - statistics
---
This is the most common [[Linear Models|linear model]] used for [[Regression]]. 

Below is a simple example when there is only one predictor variable $x$. 

![[Linear Regression-1790494447886.webp]]

# Main Mechanism

For a single predicted target value $\hat{y}$ is formed by taking a linear combination of feature inputs plus an intercept term.

For an individual observation with $p$ features, we represent the inputs as a feature [[vector]] $\mathbf{x} \in \mathbb{R}^p$ and the model's weights as a parameter vector $\mathbf{w} \in \mathbb{R}^p$:

$$\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_p \end{bmatrix}, \quad \mathbf{w} = \begin{bmatrix} w_1 \\ w_2 \\ \vdots \\ w_p \end{bmatrix}$$

The target prediction $\hat{y}$ is calculated as the [[Vector Operations#Dot Product (Inner Product)|dot product]] of the feature vector and the weight vector, plus a [[scalar]] **bias** term $b$ (also referred to as the intercept $\beta_0$):
$$\hat{y} = \mathbf{w} \cdot \mathbf{x} + b = \mathbf{w}^T \mathbf{x} + b = \sum_{j=1}^{p} w_j x_j + b$$
### Dataset Level: The Design Matrix and Matrix Multiplication

When moving from a single prediction to a dataset containing $n$ samples, we collect all feature vectors into a **Design [[Matrix]]** $\mathbf{X}$.

To absorb the scalar bias $b$ directly into the parameter vector, a standard convention is to append a column of ones ($1$) to the left side of the design matrix. This allows $b$ to act as $w_0$:

$$\mathbf{X} = \begin{bmatrix} 1 & x_{1,1} & x_{1,2} & \dots & x_{1,p} \\ 1 & x_{2,1} & x_{2,2} & \dots & x_{2,p} \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & x_{n,1} & x_{n,2} & \dots & x_{n,p} \end{bmatrix} \in \mathbb{R}^{n \times (p+1)}, \quad \mathbf{w} = \begin{bmatrix} b \\ w_1 \\ \vdots \\ w_p \end{bmatrix} \in \mathbb{R}^{p+1}$$

Using this notation, predictions for the entire dataset $\hat{\mathbf{y}} \in \mathbb{R}^n$ are computed via a single **matrix-vector multiplication**:

$$\hat{\mathbf{y}} = \mathbf{X}\mathbf{w}$$
### Noise and Error Modeling

Real-world data is rarely perfectly linear. The ground-truth target vector $\mathbf{y}$ includes random noise or unobserved variability $\boldsymbol{\varepsilon}$:

$$\mathbf{y} = \mathbf{X}\mathbf{w}^* + \boldsymbol{\varepsilon}$$

Here, $\mathbf{w}^*$ represents the true underlying parameters, and $\boldsymbol{\varepsilon} \in \mathbb{R}^n$ is an [[Residual vs Error|error]] vector. In classical statistical modeling, this noise is assumed to be independently and identically distributed (i.i.d.) [[Normal Distribution|Gaussian]] noise:

$$\varepsilon_i \sim \mathcal{N}(0, \sigma^2)$$

Linear regression aims to estimate $\mathbf{w}^*$ while accounting for this unobserved error.

Empiracally we can calculate residuals instead of errors (see [[Residual vs Error]]) and they must be approximatelly normally distributed around 0 in order for the assumtion of the [[Linear Models|linear model]] to hold.

![[Linear Regression-1790495376828.webp]]

### The Loss Function

To measure how well a given weight vector $\mathbf{w}$ fits the observed targets $\mathbf{y}$, we define a **Loss Function** $L(\mathbf{w})$ using Mean Squared Error (MSE):

$$L(\mathbf{w}) = \frac{1}{2n} \Vert{}\mathbf{X}\mathbf{w} - \mathbf{y}\Vert{}_2^2 = \frac{1}{2n} (\mathbf{X}\mathbf{w} - \mathbf{y})^T (\mathbf{X}\mathbf{w} - \mathbf{y})$$

> **The $\frac{1}{2}$ Convention:** The factor of $0.5$ is introduced purely for mathematical convenience. When taking the gradient of $L(\mathbf{w})$ with respect to $\mathbf{w}$ via the chain rule, the exponent $2$ drops down and cancels out the $\frac{1}{2}$ ($2 \cdot \frac{1}{2} = 1$), leaving a cleaner derivative expression (see in the next section).

### Analytic Solution (Normal Equation)

First, let's expand the loss function:

$$L(\mathbf{w}) = \frac{1}{2n} \left( \mathbf{w}^T \mathbf{X}^T \mathbf{X} \mathbf{w} - \mathbf{w}^T \mathbf{X}^T \mathbf{y} - \mathbf{y}^T \mathbf{X} \mathbf{w} + \mathbf{y}^T \mathbf{y} \right)$$
$$L(\mathbf{w}) = \frac{1}{2n} \left( \mathbf{w}^T \mathbf{X}^T \mathbf{X} \mathbf{w} - 2 \mathbf{y}^T \mathbf{X} \mathbf{w} + \mathbf{y}^T \mathbf{y} \right)$$

Because the loss function is convex (differentiable), we can find the exact global minimum analytically by setting the [[Derivative#Gradient]] to zero ($\nabla_{\mathbf{w}} L(\mathbf{w}) = \mathbf{0}$).

We rely on [[Differentiating Multivariate Functions Shortcuts]], namely on [[Differentiating Multivariate Functions Shortcuts#Quadratic Forms]] and [[Differentiating Multivariate Functions Shortcuts#Linear Forms]]:

- **Quadratic term:** $\frac{\partial}{\partial \mathbf{w}} (\mathbf{w}^T \mathbf{A} \mathbf{w}) = 2 \mathbf{A} \mathbf{w}$ (when $\mathbf{A}$ is symmetric, as $\mathbf{X}^T \mathbf{X}$ is).
$$\frac{\partial}{\partial \mathbf{w}} \left( \mathbf{w}^T \mathbf{X}^T \mathbf{X} \mathbf{w} \right) = 2 \mathbf{X}^T \mathbf{X} \mathbf{w}$$
- **Linear term:** $\frac{\partial}{\partial \mathbf{w}} (\mathbf{b}^T \mathbf{w}) = \mathbf{b}$.
$$\frac{\partial}{\partial \mathbf{w}} \left( 2 \mathbf{y}^T \mathbf{X} \mathbf{w} \right) = 2 \mathbf{X}^T \mathbf{y}$$
- **Constant term:** $\mathbf{y}^T \mathbf{y}$ does not depend on $\mathbf{w}$, so its derivative is $\mathbf{0}$.

Putting these together into the gradient calculation:

$$\nabla_{\mathbf{w}} L(\mathbf{w}) = \frac{1}{2n} \left( 2 \mathbf{X}^T \mathbf{X} \mathbf{w} - 2 \mathbf{X}^T \mathbf{y} + \mathbf{0} \right)$$
By setting derivative to 0 we get:
$$\mathbf{X}^T (\mathbf{X}\mathbf{w} - \mathbf{y}) = \mathbf{0}$$
$$\mathbf{X}^T \mathbf{X} \mathbf{w} = \mathbf{X}^T \mathbf{y}$$
Solving for $\mathbf{w}$ yields the **Normal Equation**:
$$\mathbf{w} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$$

- **Invertibility Condition:** For the inverse matrix $(\mathbf{X}^T \mathbf{X})^{-1}$ to exist, the matrix $\mathbf{X}^T \mathbf{X}$ must be invertible (non-singular). This requires that the **columns of $\mathbf{X}$ must be linearly independent** (no perfect multicollinearity) and that there are more samples than features ($n \ge p + 1$).

### The [[Gradient Descent]] Approach

When $\mathbf{X}$ is extremely large (e.g., millions of rows/features), computing $(\mathbf{X}^T \mathbf{X})^{-1}$ becomes computationally expensive ($O(p^3)$) or numerically unstable.

**Gradient Descent** offers an iterative alternative. Instead of solving for $\mathbf{w}$ in one step, it starts with an initial random guess $\mathbf{w}^{(0)}$ and iteratively updates the parameters in the direction opposite to the gradient (the direction of steepest descent):

$$\mathbf{w}^{(t+1)} = \mathbf{w}^{(t)} - \alpha \nabla_{\mathbf{w}} L(\mathbf{w}^{(t)})$$

$$\mathbf{w}^{(t+1)} = \mathbf{w}^{(t)} - \frac{\alpha}{n} \mathbf{X}^T (\mathbf{X}\mathbf{w}^{(t)} - \mathbf{y})$$

Where $\alpha > 0$ is the **learning rate** controlling step size. The algorithm repeatedly adjusts weights until convergence, reaching the exact same global minimum as the analytic solution without inverting a matrix.