---
tags:
  - ML
---
**Regularization** is a set of techniques used in [[Machine Learning Concepts|Machine Learning]] to prevent **overfitting** by penalizing complex models.

When a model overfits, it memorizes noise and exact patterns in the training data rather than learning generalizable rules. Regularization modifies the learning algorithm or loss function to keep model parameters smaller, simpler, or constrained, trading a tiny bit of training accuracy for significantly better performance on unseen data.

## Penalty-Based Regularization (Explicit)

These methods directly modify the loss function by adding a penalty term that scales with the size of the model's parameters (weights $\mathbf{w}$).

$$\text{Total Loss} = \text{Loss}(\mathbf{y}, \hat{\mathbf{y}}) + \lambda \cdot \Omega(\mathbf{w})$$

where $\lambda \ge 0$ is the regularization strength hyperparameter, and $\Omega(\mathbf{w})$ is the penalty term.
### L1 Regularization (Lasso)

- **Penalty:** Sum of absolute values of weights: $\Omega(\mathbf{w}) = \Vert{}\mathbf{w}\Vert{}_1 = \sum \vert{}w_i\vert{}$
- **Behavior:** Forces less important weight coefficients to become **exactly zero**.
- **Key Characteristic:** Acts as built-in **feature selection**, yielding sparse models.
- **Best Used When:** You have high-dimensional data with many redundant or irrelevant features.

### L2 Regularization (Ridge)

- **Penalty:** Sum of squared weights: $\Omega(\mathbf{w}) = \Vert{}\mathbf{w}\Vert{}_2^2 = \sum w_i^2$
- **Behavior:** Shrinks weights evenly toward zero without setting them strictly to zero.
- **Key Characteristic:** Prevents any single feature from dominating the predictions.
- **Best Used When:** Features are highly correlated (multicollinearity) or when all features likely contribute small amounts of signal.

### Elastic Net

- **Penalty:** Linear combination of L1 and L2 penalties: $\Omega(\mathbf{w}) = r \sum \vert{}w_i\vert{} + \frac{1-r}{2} \sum w_i^2$
- **Behavior:** Combines feature selection (L1) with group selection stability (L2).
- **Best Used When:** $p \gg n$ (features heavily outnumber samples) or when multiple features are strongly correlated.

## Why Different Regularization Types Do What They Do

If we minimize [[Loss vs Metric|loss]] without limits, the model sets weights to whatever values fit every single training point, including noise which might lead to higher coefficients than we would like to have. 

To prevent this, we impose a rule: **"Find the smallest training loss, but you are only allowed a limited total budget of weight magnitude."**

Mathematically, this budget constraint is written as:

$$\text{Minimize } \text{Loss}(w) \quad \text{subject to } \vert{}w_1\vert{} + \vert{}w_2\vert{} \le C$$

The form of this constraint is defined by the type of regularization as described above which essentially use different [[Vector Norm|vector norms]].

This budget forms a physical boundary in space:

- For **L1**, $\vert{}w_1\vert{} + \vert{}w_2\vert{} \le C$ defines a **diamond** region.
- For **L2**, $w_1^2 + w_2^2 \le C^2$ defines a **circle** region.

![[Regularization-1790541378538.webp]]

## What the Penalty Does to a Curve

Using an example of fitting a polynomial to a curve we can see the effect of regularization on the fitted line and on the coefficients:

![[Regularization-1790541484057.webp]]

## Structural & Architectural Regularization

Commonly used in deep learning models to constrain capacity during training.

- **Dropout:** Randomly deactivates a fraction $p$ of neurons during each training step. Forces the [[Neural Network]] to learn redundant representations rather than relying on specific co-adapted paths.
- **DropConnect:** Similar to Dropout, but sets individual weight connections to zero rather than entire node activations.
- **Early Stopping:** Monitors performance on a validation set and stops training as soon as validation loss begins to increase, preventing the model from fitting late-stage noise.

## Data & Implicit Regularization

These methods regularize the [[Neural Network]] implicitly by introducing variance or constraints into the data pipeline or optimization path.

- **Data Augmentation:** Applies transformations (flips, rotations, scaling, noise injection) to training samples, effectively expanding dataset size and forcing invariant feature representations.
- **Batch Normalization:** Normalizes layer inputs per mini-batch. While primarily meant for training stability, the batch-wise mean and variance introduce slight stochastic noise that acts as a mild regularizer.
- **Label Smoothing:** Replaces hard binary targets ($0$ or $1$) with softened targets (e.g., $0.05$ and $0.95$), preventing the network from becoming overly confident in its logit predictions.