---
tags:
  - ML
---
In [[Machine Learning Concepts|Machine Learning]], the ultimate goal is to build a model that **generalizes well to unseen data**: meaning it performs accurately on new data, not just the data it learned from.

Split and cross-validation mechanics implement the labeled side of [[Validation Strategy]]. To prevent **overfitting** (where a model simply memorizes the training data), data is split into distinct sets.

## Train vs Test Sets

When building a model, the original dataset is typically split into two primary parts:

- **Training Set (~70%–80% of data):** Used by the machine learning algorithm to learn patterns, weights, or relationships between input features and target outputs.
- **Test Set (~20%–30% of data):** Kept completely separate during training. It acts as a final, unbiased evaluation to measure how well the trained model generalizes to new, unseen real-world data.

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
1. Split the training data into $K$ equal-sized subsets (folds), commonly $K=5$ or $K=10$.
2. Train the model $K$ times.
3. In each iteration, use $K-1$ folds for training and the remaining $1$ fold for validation.
4. Calculate the average score across all $K$ iterations to get a stable performance metric.
### Common Types of Cross-Validation

- **Stratified $K$-Fold:** Ensures class distribution (e.g., 80% class A, 20% class B) is identical in every fold: essential for imbalanced datasets.
- **Time-Series Split:** Respects chronological order so future data is never used to predict past data.
- **Leave-One-Out (LOOCV):** Uses $K = N$ (where $N$ is total sample size). High computational cost, but useful for tiny datasets.
- **ShuffleSplit**: by specifying a fracture from the dataset and number of draws the algorithm takes validation samples and put them back into the main dataset, and then repeats the process agains as many times as specified. Same examples can appear in different validations sets.
- **Group K-fold**: Used in datasets where multiple observations belong to the same underlying entity or group. Prevents data leakage between the training and validation sets by keeping groups in the same subset. 

## Sizing the Split

### Validation Size and Confidence Intervals

Each validation fold (or holdout validation / test set) is an **estimation sample** for the scoring metric. If that sample is tiny, fold scores wobble and score differences are hard to trust. Use CIs and fold SD here for **sizing and stability**, not as a formal way to declare a winning model: ranking under noise belongs in [[Model Selection#Comparing Many Models|Model Selection]].

For [[Classification Metrics#Accuracy]] (or any success/failure rate) on independent rows, treat the score as a binomial proportion $\hat{p}$ with evaluation size $n_{\mathrm{val}}$ (rows in that validation fold or holdout). The usual [[Wald Interval]] ([[Confidence Interval]]) uses the [[Sampling Distribution|standard error]]:

$$\mathrm{SE}(\hat{p}) = \sqrt{\frac{\hat{p}(1-\hat{p})}{n_{\mathrm{val}}}}$$

and the interval $\hat{p} \pm z_{1-\alpha/2}\,\mathrm{SE}(\hat{p})$. Here $E$ is the **margin of error**: the half-width of that interval, the largest distance from $\hat{p}$ you are willing to tolerate at a confidence level ($1-\alpha$).

Set the half-width equal to the target margin and solve for $n_{\mathrm{val}}$:

$$z_{1-\alpha/2}\,\mathrm{SE}(\hat{p}) = E
\quad\Rightarrow\quad
z_{1-\alpha/2}\sqrt{\frac{p(1-p)}{n_{\mathrm{val}}}} = E
\quad\Rightarrow\quad
n_{\mathrm{val}} \approx \frac{z_{1-\alpha/2}^{2}\,p(1-p)}{E^{2}}$$

Use a planning value of $p$ (often the conservative $p = 0.5$, which maximizes $p(1-p)$). After you observe data, plug in $\hat{p}$ only to *describe* the interval, not to re-plan $n$ retrospectively without care.

Heuristics at 95% ($z \approx 1.96$, $p = 0.5$):

| Target Margin $E$ | Approx. $n_{\mathrm{val}}$ |
| --- | ---: |
| $\pm 0.05$ | ~384 |
| $\pm 0.03$ | ~1,068 |
| $\pm 0.02$ | ~2,401 |

### Caveats

- When the empirical proportion is $\hat{p} = 0$ or $\hat{p} = 1$ (every validation row wrong, or every row correct), the [[Wald Interval|Wald]] SE is zero and the interval collapses to a point even though uncertainty remains. Prefer a [[Wilson Score Interval]]: it centers the CI using an adjusted proportion that pulls extreme $\hat{p}$ toward $1/2$, so the interval stays wide and better covered near the boundaries. For an exact binomial CI, use [[Clopper-Pearson Interval]] (invert binomial tests) rather than the normal approximation.
- When the metric is not a simple proportion (F1, AUC, etc.), the sizing formula above is only a rough guide for how large $n_{\mathrm{val}}$ needs to be. Report uncertainty with [[Bootstrapping|bootstrap]] CIs or a metric-specific variance estimator instead.
- In $K$-fold, each fold validates on about $N/K$ rows. Size folds so **per-fold** $n_{\mathrm{val}}$ is large enough for useful precision. The average CV score is stabler than a single fold, but folds are **dependent**: their training sets overlap heavily, so fold scores are not i.i.d. samples. Reporting the CV mean together with the **standard deviation of the $K$ fold scores** is a useful **descriptive** picture of fold-to-fold variability; it is not a calibrated [[Confidence Interval]] that assumes independent folds. For interval estimates that respect dependence, prefer nested CV or [[Bootstrapping|bootstrap]] schemes.
- If stakeholders care about the final reported number, size the held-out **test** set for a reportable CI as well.
- Narrowing a CI sizes how precisely you know *one* score. Deciding whether one model beats another under sampling noise is a [[Model Selection#Comparing Many Models|Model Selection]] problem (with [[Power Analysis]] when you plan for a minimum detectable difference).

### Training Size and Learning Curves

The training slice must be large enough that the model still has room to improve when more data is the goal, or large enough that you can *see* it has already saturated.

A **learning curve** plots train score and validation (or CV) score against training size $n_{\mathrm{train}}$:

- A rising validation curve means more rows of the same kind still buy improvement.
- A flat validation curve near a floor means capacity limits or label noise dominate: collecting more similar data helps little. That floor can approach the **Bayes error rate** (irreducible error): the best average error any model can achieve with these features and this label noise.
- Different model families plateau at different $n$ (e.g. linear models earlier than tree ensembles or deep nets). Do not assume one global “enough data.”

For the learning-curve figure and how more data lowers variance until the plateau, see [[Bias and Variance#Lowering Variance|Bias and Variance]].

### Fixed Budget Trade-off

Under fixed total $N$, enlarging $n_{\mathrm{val}}$ (or choosing larger $K$ so each fold is bigger) sharpens the score estimate from [[#Validation Size and Confidence Intervals]], but shrinks $n_{\mathrm{train}}$ and can hurt high-capacity models that are still climbing their learning curves.

Practical pattern:

1. Hold out a **final test set** and do not use it to pick models or tune hyperparameters. That set is for the number you report to stakeholders. Size it with the same CI logic as validation ($n$ large enough that the metric’s margin of error is small enough to act on), **or**, if the real decision is a live business experiment comparing variants, size that holdout the way you would size an [[AB Testing|A/B test]] ([[Power Analysis]]).
2. On the remainder, choose $K$ / validation fraction so **per-fold** $n_{\mathrm{val}}$ meets a CI (or power) target **and** learning curves for the families you care about are not still steep on the train side.
3. If both cannot be met, collect more data or narrow the model menu.

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

