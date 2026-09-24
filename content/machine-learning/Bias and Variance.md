---
tags:
  - statistics
  - ML
---
Bias and variance are two fundamental sources of error in statistical modeling and [[Machine Learning Concepts|Machine Learning]] that govern how well a model generalizes to unseen data.

- **Bias:** Error introduced by simplifying assumptions in the algorithm. High bias causes the model to miss relevant relations between features and target outputs (**underfitting**).
- **Variance:** Error caused by the model's sensitivity to small fluctuations in the training set. High variance causes the algorithm to model the random noise in the training data rather than the intended outputs (**overfitting**).

# Statistical Decomposition

In terms of [[Mean Squared Error]], bias and Variance are its two components. See [[Mean Squared Error#Bias-Variance Decomposition]]. 

### Consequence to Interpretation

- **Variance** measures how much the estimate $\hat{\theta}$ fluctuates around its average location across different samples (spread/precision).
- **Bias** measures how far the average estimate $\mathbb{E}[\hat{\theta}]$ falls from the true value $\theta$ (systematic offset/accuracy).
# Managing the Bias-Variance Tradeoff

Below is an example showing the validation curve for polynomial model with increasing complexity. 
![[Bias and Variance-1790282500308.webp]]

We can see that having a simple line (1-degree polynomial produces a poor model) with both train and test error being high (high Bias). However they are at the same level which means that Variance is not as defined as Bias.

Making it a second-degree polynomial dramatically imporves both the train and the test error. If we were to increase the degree of polynomial even further, the train error will reduce but now we are modeling the noise of the training dataset which does not generalize into the unknown data. Which is why the test error increases and we have high Variance.

In this particular example we should favor a configuration at which the test error is the lowest. 

It is also worth looking at the variance of the error and compare it between train and test. 
## Lowering Bias

Increase model capacity (e.g., use a [[Neural Network]] or polynomial features), drop heavy regularization penalties, or engineer richer inputs. 
## Lowering Variance

Simplify the model (feature selection/pruning), apply [[regularization]] ($L_1$/$L_2$), or use [[ensemble methods]] like Random Forests (bagging).

Another way to reduce Variance is the obtain more data to train on.

![[learning_curve.gif]]

 With more data coming even complex model can generalize well because it fits many points at once and noise has less weight now. We can observe decreasing of the test error while the train error can even increase at the beginning. 
 
Increasing of the train error is cause by more variability between new data points. 

Eventually the test error plateaus and the model reaches the point of Bayes error rate (irreducible noise). This is the point where adding more date is no longer beneficial to the model performance but instead increases the costs. 

