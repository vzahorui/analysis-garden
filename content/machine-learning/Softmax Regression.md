---
tags:
  - ML/classification
---
Softmax Regression is a generalization of [[Logistic Regression]] to multiple classes.
## How Binary Logistic Regression Extends to Multi-Class

In binary logistic regression, the model learns a single vector of weights $W$ to compute a single linear score $z$, which is then converted into a probability using the **Sigmoid function**:

$$P(y=1) = \frac{1}{1 + e^{-z}}$$

For a problem with $K$ classes (where $K \ge 3$), the model learns **$K$ separate sets of weights** ($W_1, W_2, \dots, W_K$), generating $K$ distinct raw linear scores ($z_1, z_2, \dots, z_K$):

$$z_k = \beta_{k,0} + \beta_{k,1} x_1 + \beta_{k,2} x_2 + \dots + \beta_{k,n} x_n$$

To convert these $K$ arbitrary real-valued scores into a valid probability distribution (where all values lie between 0 and 1, and sum to 1), we replace the [[Sigmoid function]] with the [[Softmax Function]]. 

In this case to the target categorical variable [[Encoding Categorical Variables#One-Hot Encoding (OHE)]] needs to be applied.

## Loss Function

For Softmax, the loss function generalizes from Binary Cross-Entropy to **Categorical [[Cross-Entropy]]**:
$$\mathcal{L} = -\sum_{k=1}^K y_k \ln(\hat{p}_k)$$

## What About the Threshold of Probability of a Class?

In Logistic Regression we need to select a [[Logistic Regression#Decision Boundary]]. 

By default, Softmax assigns an observation to whichever class receives the **highest predicted probability**:

$$\hat{y} = \arg\max_{k \in \{1, \dots, K\}} P(y = k \mid \mathbf{x})$$

Because all exponentiated terms in Softmax share the exact same denominator ($\sum_{j=1}^K e^{z_j}$), the class with the largest probability is simply the class with the **largest raw linear score ($z_k$)**:

$$\hat{y} = \arg\max_{k} z_k$$

### What does the "threshold" look like implicitly?

In a 3-class problem with equal class weighting, the implicit threshold to win a class is **not fixed**:

- If probabilities are evenly distributed ($0.34, 0.33, 0.33$), a class can win with just **$34\%$ probability**.
- If two classes dominate ($0.49, 0.49, 0.02$), a class needs **$>49\%$ probability** to win.

### Using Custom Thresholds in Softmax

Just like in binary logistic regression, the default rule ($\text{argmax}$) assumes:

1. **Symmetric misclassification costs** (e.g., predicting Class A when it's Class B costs the same as the inverse).
2. **Balanced class distributions**.

When these assumptions fail, you apply **custom thresholds** or **decision rules**.
