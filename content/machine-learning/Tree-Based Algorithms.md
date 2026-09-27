---
tags:
  - ML
aliases:
  - decision trees
  - decision tree
---
Tree-based algorithms are a class of supervised machine learning algorithms that recursively partition data into smaller, more homogeneous subsets based on decision rules. They are widely used for both [[classification]] and [[regression]] due to their interpretability, ability to handle non-linear relationships, and minimal requirements for data preprocessing.

## Core Mechanics: How Decision Trees Work

A decision tree constructs a flowchart-like structure consisting of:

- **Root Node:** The top-level node containing the entire dataset, where the first split occurs.
- **Internal / Decision Nodes:** Intermediate points where a feature condition is evaluated to branch further.
- **Leaf (Terminal) Nodes:** End points that output the final prediction (a class category or a continuous mean value).

![[Tree-Based Algorithms-1790537250567.webp]]

### Splitting Criteria (Impurity Metrics)

At each node, the algorithm evaluates all available features and candidate split thresholds to choose the split that maximizes **information gain** (i.e., minimizes impurity in the child nodes):

1. **Gini Impurity (Classification):** Measures the probability of misclassifying a randomly chosen element from the set.
$$Gini = 1 - \sum_{i=1}^{k} p_i^2$$
2. **[[Entropy]] & Information Gain (Classification):** Measures disorder/uncertainty within a node.

$$Entropy = -\sum_{i=1}^{k} p_i \log_2(p_i)$$
3. **Variance Reduction / [[Mean Squared Error]] (Regression):** Splits are chosen to minimize the weighted average variance (or MSE) of the target variable across the child nodes.

In practice, Gini Impurity and Entropy yield near-identical decision trees but Gini is faster to calculate.
#### Selection Rules per Gini Impurity

A node of one class has $G = 0$. A node split evenly between two classes has $G = 1/2$.

The impurity of a candidate is the weighted average of its children,

$$G_{\mathrm{split}} = \frac{n_L}{n_t} G_L + \frac{n_R}{n_t} G_R$$

where $n_t$ is the number of samples at the node being split. The tree chooses the feature and threshold with the smallest $G_{\mathrm{split}}$.

Below is the illustration of how Gini selects splits for the example from above.

![[Tree-Based Algorithms-1790537184053.webp]]

## Common Tree-Based Algorithms

Tree models have evolved from single interpretable trees to complex ensemble approaches that combine multiple trees to improve accuracy and generalizability.

| **Algorithm**                                | **Ensemble Type**               | **Core Mechanism & Characteristics**                                                                                                                                                                                            |
| -------------------------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Decision Trees**                           | Single Model                    | Creates a single explicit rule hierarchy. Highly interpretable and fast, but prone to **high [[Bias and Variance\|variance]]** and **overfitting** on complex tasks.                                                            |
| [[Random Forest]]                            | Bagging (Bootstrap Aggregating) | Trains hundreds of deep, independent decision trees in parallel using bootstrapped samples of data and random feature subsets. Aggregates predictions via voting (classification) or averaging (regression) to reduce variance. |
| **Extra Trees (Extremely Randomized Trees)** | Bagging                         | Similar to Random Forests, but chooses split thresholds completely at random rather than optimizing them, offering faster training and slightly stronger variance reduction.                                                    |
| **Gradient Boosting Machines (GBM)**         | Boosting                        | Builds trees **sequentially**. Each new tree is trained to fit the pseudo-residuals ([[Derivative\|gradients]] of the loss function) of the previous aggregated trees. Offers high accuracy but is sensitive to noise.          |
| **XGBoost, LightGBM, CatBoost**              | Optimized Boosting              | Production-grade implementations of Gradient Boosting featuring second-order loss approximations, [[Regularization\|regularized]] tree objectives, histogram-based splitting, and built-in handling for categorical features.   |

## Key Strengths & Limitations

### Advantages

- **Non-Linear Patterns:** Captures complex, non-linear interactions without requiring manual feature engineering or polynomial expansions.
- **Minimal Preprocessing:** Does not require feature scaling (normalization/standardization) because splits depend strictly on relative ordering rather than absolute scale.
- **Missing Value & Categorical Support:** Handles mixed data types and missing values natively (especially algorithms like CatBoost or XGBoost).
- **Interpretability:** Single decision trees can be rendered directly as flowchart diagrams. Ensemble models provide feature importance scores (e.g., Gini importance, SHAP values).
### Disadvantages

- **Overfitting:** Single decision trees can easily grow too deep and memorize noisy training data (mitigated by pruning or using ensembles).
- **Instability:** Small variations in data can alter the root split, leading to a completely different tree structure.
- **Extrapolation Limitations:** Tree models cannot extrapolate beyond the range of target values seen in the training data (predictions outside the bounding box default to leaf constants).
- **Axis-Aligned Splits:** standard decision trees evaluate one feature at a time, creating orthogonal boundary steps that struggle with diagonal decision boundaries.

## Hyperparameter Tuning

To prevent overfitting and control model complexity, adjust the following key hyperparameters:

1. **`max_depth`:** Limits the maximum distance between the root node and any leaf node. Lower values prevent trees from memorizing training samples.
2. **`min_samples_split`:** The minimum number of samples required in an internal node before it can be split.
3. **`min_samples_leaf`:** The minimum number of samples required to form a valid leaf node. Smooths predictions, particularly in regression tasks.
4. **`max_features`:** The number of randomly selected candidate features to evaluate at each split (crucial for Random Forests).
5. **`learning_rate` / `eta` (Boosting models):** Scales the contribution of each added tree to prevent individual trees from over-dominating the prediction.