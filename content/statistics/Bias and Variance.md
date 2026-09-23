---
tags:
  - statistics
---
Bias and variance are two fundamental sources of error in statistical modeling and machine learning that govern how well a model generalizes to unseen data.

- **Bias:** Error introduced by simplifying assumptions in the algorithm. High bias causes the model to miss relevant relations between features and target outputs (**underfitting**).
- **Variance:** Error caused by the model's sensitivity to small fluctuations in the training set. High variance causes the algorithm to model the random noise in the training data rather than the intended outputs (**overfitting**).

# Statistical Decomposition

In terms of [[Mean Squared Error]], bias and Variance areits two components. See [[Mean Squared Error#Bias-Variance Decomposition]]. 

### Consequence to Interpretation

- **Variance** measures how much the estimate $\hat{\theta}$ fluctuates around its average location across different samples (spread/precision).
- **Bias** measures how far the average estimate $\mathbb{E}[\hat{\theta}]$ falls from the true value $\theta$ (systematic offset/accuracy).
# Managing the Bias-Variance Tradeoff

- **To lower Bias:** Increase model capacity (e.g., use a [[Neural Network]] or polynomial features), drop heavy regularization penalties, or engineer richer inputs.

- **To lower Variance:** Gather more training data, simplify the model (feature selection/pruning), apply [[regularization]] ($L_1$/$L_2$), or use [[ensemble methods]] like Random Forests (bagging).