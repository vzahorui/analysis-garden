---
tags:
  - ML
---
**Random Forest** is an ensemble [[Machine Learning Concepts|Machine Learning]] algorithm that combines hundreds of individual [[Tree-Based Algorithms|decision trees]] to make a single, highly accurate prediction. By aggregating many "weak" or prone-to-overfitting decision trees into a collective "forest," the model dramatically reduces variance and avoids overfitting without sacrificing predictive power.

## Core Mechanics: How Random Forests Work

Random Forests build on the concept of **Bagging** ([[Bootstrapping|Bootstrap]] Aggregating) and introduce **Random Feature Subspace Selection**.

The training process follows four key steps:

### Bootstrap Sampling (Bagging)

Given a dataset with $N$ samples, the algorithm creates $T$ distinct subsets by sampling $N$ observations _with replacement_ (bootstrapping) for each tree. On average, each bootstrapped dataset contains roughly 63.2% of the unique original rows; the remaining 36.8% are left out as **Out-of-Bag (OOB)** samples.
### Random Feature Subspace Selection

When splitting a node inside any individual tree, the algorithm does not evaluate all $P$ features. Instead, it selects a random subset of $m$ features ($m \ll P$) as candidates for that specific split:

- **Classification default:** $m = \sqrt{P}$
- **Regression default:** $m = \frac{P}{3}$

### Full Tree Growth

EAch tree is grown deep to its maximum limit (or until a minimum leaf size is reached) **without pruning**. Individual trees have high variance and overfit their specific bootstrap sample, but they are decorrelated from one another.
    
### Aggregation (Voting / Averaging)
 
 To make a prediction for a new data point, the input is passed through all $T$ trees:
  - **Classification:** Majority vote across all tree predictions.
  - **Regression:** Mean (average) of all tree predictions.

## Why Random Forest Outperforms a Single Decision Tree

Single decision trees suffer from igh [[Bias and Variance|variance]]: a slight change in training data can drastically alter the root split and change the entire tree topology.

Random Forest solves this using the [[Law of Large Numbers]]:

- **Variance Reduction:** If you average $T$ independent models, each with variance $\sigma^2$, the variance of the average is $\frac{\sigma^2}{T}$.
- **Decorrelation is Key:** If the trees were correlated (e.g., using all features at every split), a dominant feature would be chosen at the root of every tree, making them make identical mistakes. Forcing each split to consider only a random subset of features decorrelates the trees, lowering the covariance term between tree outputs.

## Key Features & Internal Mechanisms

### Out-of-Bag (OOB) Error Estimation

Because each tree is trained on ~63% of the data, the remaining ~37% (Out-of-Bag) can serve as a built-in validation set. Evaluating each sample using only the trees that _did not_ see it during training provides an unbiased performance estimate without needing a separate cross-validation split.

### Feature Importance Measures

Random Forest provides two main ways to measure feature importance:

1. **Mean Decrease in Impurity (MDI / Gini Importance):** Measures the total gain in purity (Gini or Entropy reduction) brought by splits on a given feature across all trees.
2. **Mean Decrease in Accuracy (MDA / Permutation Importance):** Randomly shuffles (permutes) the values of a single feature in the OOB samples and records the drop in prediction accuracy. A steep drop indicates a critical feature.

## Key Hyperparameters

|**Hyperparameter**|**Description**|**Impact**|
|---|---|---|
|`n_estimators`|Number of trees in the forest.|Higher is generally better (stabilizes predictions), but increases computation time. Diminishing returns occur beyond 100–500 trees.|
|`max_features`|Size of the random feature subset evaluated at each split.|Lowering $m$ decorrelates trees further (reduces variance), but may increase individual tree error (increases bias).|
|`max_depth`|Maximum depth allowed for individual trees.|Restricts tree size. Usually left unrestricted or set high, as bagging inherently prevents overfitting.|
|`min_samples_leaf`|Minimum number of samples required at a terminal node.|Higher values smooth predictions and reduce variance in noisy datasets.|
|`bootstrap`|Whether to use bootstrap samples or the full dataset.|Setting to `False` uses the full dataset for every tree (similar to Extra Trees).|

## Pros and Cons

### Advantages

- **High Accuracy & Robustness:** Performs exceptionally well out-of-the-box on tabular datasets without heavy tuning.
- **Resistant to Overfitting:** Adding more trees does not cause overfitting; it simply stabilizes the ensemble's variance reduction.
- **Minimal Preprocessing:** Handles non-linearities, interactions, and mixed data types (numerical and categorical) without scaling or normalization.
- **Parallelizable:** Trees are completely independent and can be trained across multiple CPU cores simultaneously.
### Limitations

- **Black Box Nature:** While individual trees are simple flowcharts, aggregating 500 deep trees makes direct visual interpretation difficult.
- **Memory & Inference Overhead:** Storing and scoring large ensembles requires significantly more memory and computational power than linear models or single decision trees.
- **Extrapolation Boundaries:** Cannot predict continuous values outside the range of the training set target values.