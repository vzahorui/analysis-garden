---
tags:
  - statistics
---
Covariance measures how two [[Set Theory#Random Variable|random variables]] change together. If higher values of one variable generally correspond to higher values of another, their covariance is positive; if higher values of one correspond to lower values of the other, it is negative.

When extended to a random [[vector]] $X = [X_1, X_2, \dots, X_n]^T$ with [[Expectation|mean]] vector $\mu = E[X]$, the formal definition is the expected value of the outer product of their deviations from the mean:

$$\Sigma = \text{Cov}(X) = E\left[ (X - \mu)(X - \mu)^T \right]$$
Here $X_i$ is a random variable. 

The resulting $n \times n$ covariance [[matrix]] $\Sigma$ organizes all pairwise covariances:

- **Diagonal elements ($\Sigma_{ii}$):** The variance of each individual coordinate, $\text{Var}(X_i)$.
- **Off-diagonal elements ($\Sigma_{ij}$ where $i \neq j$):** The covariance between coordinates $X_i$ and $X_j$, showing how strongly and in what direction they co-vary.

## Variance of Linear Combination

If you define a new scalar random variable $Y$ as a linear combination of the coordinates of $X$ using a constant vector of weights $v = [v_1, v_2, \dots, v_n]^T$:

$$Y = v^T X = v_1 X_1 + v_2 X_2 + \dots + v_n X_n$$

The variance of $Y$ is given directly by $v^T \Sigma v$:

$$\text{Var}(Y) = \text{Var}(v^T X) = v^T \Sigma v$$
### Step-by-Step Mathematical Derivation

1. **Start with the definition of variance for a scalar:**
$$\text{Var}(Y) = E\left[(Y - E[Y])^2\right]$$
2. **Substitute $Y = v^T X$ and $E[Y] = E[v^T X] = v^T \mu$:**
$$Y - E[Y] = v^T X - v^T \mu = v^T (X - \mu)$$
3. **Square the scalar difference using transpose properties ($a^2 = a \cdot a = a \cdot a^T$):**
$$(Y - E[Y])^2 = \left( v^T (X - \mu) \right) \left( v^T (X - \mu) \right)^T$$
$$(Y - E[Y])^2 = v^T (X - \mu) (X - \mu)^T v$$
4. **Apply the expectation operator:**
$$\text{Var}(Y) = E\left[ v^T (X - \mu) (X - \mu)^T v \right]$$
5. **Pull non-random constants $v$ outside the expectation:**
$$\text{Var}(Y) = v^T E\left[ (X - \mu) (X - \mu)^T \right] v$$
6. **Substitute the definition $\Sigma = E\left[ (X - \mu) (X - \mu)^T \right]$:**
$$\text{Var}(Y) = v^T \Sigma v$$

### Geometric and Practical Interpretations

- **Variance Along a Projection Line:** If $v$ is a unit vector ($\Vert{}v\Vert{} = 1$), it defines a specific direction in $n$-dimensional space. The [[scalar]] $v^T \Sigma v$ gives the spread (variance) of the data points when projected onto the line passing through that direction $v$.
- **[[Principal Component Analysis]] (PCA):** PCA finds directions $v$ that maximize $v^T \Sigma v$ subject to $\Vert{}v\Vert{} = 1$. The direction that yields the maximum variance is the first principal component, which corresponds to the [[Eigenvectors and Eigenvalues|eigenvector]] of $\Sigma$ associated with its largest eigenvalue.
- **Positive Semi-Definiteness:** Because $v^T \Sigma v$ represents a variance, it can never be negative ($\text{Var}(Y) \ge 0$). This proves mathematically that every valid covariance matrix $\Sigma$ is positive semi-definite.