---
tags:
  - ML
---
In machine learning, the ultimate goal is to build a model that **generalizes well to unseen data**—meaning it performs accurately on new data, not just the data it learned from.

To achieve this and prevent **overfitting** (where a model simply memorizes the training data), data is split into distinct sets.

## Train vs Test Sets

When building a model, the original dataset is typically split into two primary parts:

- **Training Set (~70%–80% of data):** Used by the machine learning algorithm to learn patterns, weights, or relationships between input features and target outputs.
- **Test Set (~20%–30% of data):** Kept completely separate during training. It acts as a final, unbiased evaluation to measure how well the trained model generalizes to new, unseen real-world data.

```
Total Dataset
├───────────────────────────────┬─────────────────┐
│         Training Set          │    Test Set     │
│    (Model learns patterns)    │ (Final Eval)    │
└───────────────────────────────┴─────────────────┘
```

### The Validation Set

If you evaluate different models or tune hyperparameters (like learning rates or tree depth) using the **test set**, the test set indirectly influences training, leading to **data leakage**. To avoid this, a three-way split is often used:
- **Train Set:** Trains the model.
- **Validation Set:** Used to compare models and fine-tune hyperparameters.
- **Test Set:** Used strictly once at the end to e valuate final performance.
## What is Cross-Validation?

A single train/validation split has a flaw: **it relies on a single random cut**. If your validation set happens to be unusually easy or hard, your performance estimates will be skewed.

**Cross-Validation (CV)** solves this by rotating through different portions of the dataset for training and validation, ensuring every data point gets evaluated.
### K-Fold Cross-Validation

The most common technique is **$K$-Fold Cross-Validation**:
1. Split the training data into $K$ equal-sized subsets (folds)—commonly $K=5$ or $K=10$.
2. Train the model $K$ times.
3. In each iteration, use $K-1$ folds for training and the remaining $1$ fold for validation.
4. Calculate the average score across all $K$ iterations to get a stable performance metric.
### Common Types of Cross-Validation

- **Stratified $K$-Fold:** Ensures class distribution (e.g., 80% class A, 20% class B) is identical in every fold—essential for imbalanced datasets.
- **Time-Series Split:** Respects chronological order so future data is never used to predict past data.
- **Leave-One-Out (LOOCV):** Uses $K = N$ (where $N$ is total sample size). High computational cost, but useful for tiny datasets.
- ShuffleSplit: by specifying a fracture from the dataset and number of draws the algorithm takes validation samples and put them back into the main dataset, and then repeats the process agains as many times as specified. Same examples can appear in different validations sets.

### Watch for

Standard deviation of the model score across folds tells you how certain the model generalization performance is.

We can also compare the confidence interval from CV between different models to determine whether they are within the error bands of one another.
## What If the Model Fails on Test

When a model scores well during Cross-Validation (CV) but fails on the held-out test set, it indicates a **generalization failure**. Here are common causes:
### Data Leakage

Data leakage occurs when information from the validation fold spills into the training folds, or when test information contaminates the overall preprocessing pipeline. 
#### Global Feature Scaling or Imputation

This is the case when scaling features (e.g., via `StandardScaler` is scikit-learn) or imputing missing values on the _entire dataset_ before performing $K$-Fold CV. 

Instead, transformersshould only be fit on the training folds within each CV iteration. Use scikit-learn `Pipeline` objects so preprocessing steps are re-fit strictly inside each fold.
#### Target Encoding Outside the CV Loop

Simiarly to the Feature Scaling, this happens when encoding categorical variables using target statistics calculated across all samples.

Instead, compute target encodings inside each CV fold or inside a pipeline step.
#### Duplicate or Highly Correlated Samples (Group Leakage)

Multiple rows can originate from the same subject, user, or device (e.g., multiple images of the same patient). Standard $K$-Fold randomly distributes these rows across train and validation folds, causing the model to "memorize" subjects.

Use **`GroupKFold`** or **`GroupShuffleSplit`** to ensure all samples from a single subject/group stay strictly in either the training or validation fold.

### Train-Test Distribution Shift (Data Drift)

If the distributions of input features ($X$) or targets ($y$) in the test set differ from the training set, a model tuned on the training data will underperform on the test set.
 
 **How to Diagnose & Fix**:

- **Check Feature Distributions:** Run [[Kolmogorov-Smirnov Test]] or compare summary statistics (mean, variance, quantiles) between the training set and test set.
- **ML way**: 
    -  Label train data as 1, and test data as 0 and perform [[Machine Learning Concepts|Machine Learning]] classification on it. If the [[AUC]] is around 0.5 then the data distribution is approximately the same between the two sets. 
    - Unsupervised learning (via [[Principal Component Analysis|PCA]] and visualizing a [[Scatter Plot]] in 2D to see if the datapoints belonging from train and test form separate clusters. 
- **Check Strategy for Splitting:**
    - **Random Split on Time-Dependent Data:** If data has a temporal component (e.g., stock prices, user behavior over time) and you used a random split, the model used future data to predict the past during CV.
     Switch to **Time-Series Split** (`TimeSeriesSplit`) or chronological train-test splits.
    - **Class Imbalance:** If the test set has a significantly different class distribution than the training set.
     Use **Stratified $K$-Fold** (`StratifiedKFold`) to maintain class ratios consistently across all splits.

