---
tags:
  - ML
---
Model selection is the process of choosing the optimal machine learning algorithm and configuration (hyperparameters) for a given dataset and problem statement. It aims to find a model that minimizes generalization error on unseen data by navigating the [[Bias and Variance]].

Runs after [[Validation Strategy]] and [[Choice of a Scoring Metric]] are set: this note executes that evaluation plan.

## The Core Objective: Generalization

Every model selection decision trades off capacity against stability. Refer to [[Bias and Variance#Managing the Bias-Variance Tradeoff]] for the statistical mechanics.

## Validation Framework

Model selection requires an unbiased evaluation pipeline: [[Train and Test#What is Cross-Validation?|cross-validation]] for rotation of held-out scores, and [[Train and Test#Sizing the Split|split sizing]] so those scores are precise enough to trust. Keep fold membership identical across candidates ([[Pipeline Reproducibility]]).

## The Selection Workflow

Baseline Model  ──►  Model Exploration ──► Hyperparameter Tuning ──►  Final Test Evaluation
### Step 1: Baseline
Start with a simple, highly interpretable model (e.g., Linear Regression or a decision tree) to establish an minimum acceptable performance benchmark.
### Step 2: Algorithm Screening
Create diverse models from different families which can be applied to a problem at hand (often on the order of ten candidates, including a [[Dummy Estimators|dummy]] baseline):
* [[Linear Models]] / [[Regularization|Regularized]] Models (High Bias, Low Variance baseline)
* [[Tree-Based Algorithms]] ([[Random Forest]], XGBoost, LightGBM)
* [[Neural Network|Neural Networks]] / Specialized architectures

Screening many models creates ranking noise: finish with [[#Comparing Many Models]] when differences matter.
### Step 3: Hyperparameter Tuning
Once the candidate algorithms are identified, optimize their parameters using the most suited [[Objectives & Metrics|metrics]] (e.g., F1-score, RMSE, [[AUC]]):
* **Grid Search:** Exhaustive search over a fixed parameter grid.
* **Random Search:** Random sampling of parameter spaces; more efficient in high dimensions.
* **[[Bayesian Statistics|Bayesian]] Optimization:** Probabilistic search that uses prior trial evaluation history to sample optimal parameters.

The model complexity can also be tuned by looking at validation curve as in [[Bias and Variance#Managing the Bias-Variance Tradeoff]].

### Step 4: Final Model Selection

Score every candidate on **identical** [[Train and Test#What is Cross-Validation?|CV]] splits (fix seeds and export indices via [[Pipeline Reproducibility]]). Rank by the primary metric, keep a short cluster of near-best models (not only the single argmax), then decide under sampling noise with [[#Comparing Many Models]] when the gap is small.

If several models produce nearly identical results, select the simpler one (more interpretable and less computation-demanding), subject to the production constraints below.

## Comparing Many Models

Overlapping fold scores or CIs are a weak screen only. When you have roughly ten classifiers and need to pick a winner while accounting for noise, use a shortlist and paired tests on shared evaluation rows (pooled out-of-fold predictions or a fixed validation / test set).

1. **Screen:** fit diverse families plus a [[Dummy Estimators|dummy]] on the same splits; drop models clearly below the pack (and anything that loses to the dummy).
2. **Shortlist:** keep a cluster of the best (e.g. the top few within fold-to-fold noise of each other). Do not run every pairwise test on the full menu.
3. **Omnibus:** run [[Cochran’s Q Test]] on the $N \times k$ matrix of per-row correct / incorrect labels for the shortlist ($k \ge 3$). $H_0$: equal success rates across those models.
4. **Post hoc:** if Q is significant, compare pairs with [[McNemar's Test]] on discordant predictions and control the false discovery rate with the [[Multiple Hypothesis Testing#Benjamini-Hochberg (BH) Procedure|Benjamini-Hochberg]] procedure.
5. **Decide:** if nothing separates, keep the simpler / cheaper model. If one dominates on the primary metric and still meets production constraints, ship it.

### When This Workflow Applies

| Requirement | Implication |
| --- | --- |
| Same instances, paired predictions | Shared validation / test rows or aligned out-of-fold indices; do not mix different random splits ([[Train and Test]], [[Pipeline Reproducibility]]) |
| Binary outcome per row | Correct / incorrect (or a dichotomized decision). Soft scores need a different test |
| Classification (hard labels) | Natural fit. For regression or ranking metrics, use paired [[Bootstrapping\|bootstrap]], permutation tests, or similar paired comparisons instead |
| Independent rows | Group leakage (same patient / user in many rows) breaks naive pairing: use group splits and compare at group level ([[Train and Test#Common Types of Cross-Validation\|Group K-fold]]) |

Shared CV folds make scores paired across models (useful for McNemar / Q) but not independent experiments. Treat the shortlist test as confirmatory on a design frozen after screening, or nest an outer split if search volume was large.

## Evaluation Criteria Beyond Raw Metrics

While optimization relies on specific performance [[Objectives & Metrics|metrics]], production model selection must also evaluate trade-offs in real-world constraints:

| Constraint              | Consideration                                                                                                                         |
| :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **Inference Latency**   | Does the model meet real-time requirements (e.g., single tree vs. 100-tree ensemble)?                                                 |
| **Model Size / Memory** | Can it run on edge devices or budget instances?                                                                                       |
| **Interpretability**    | Is black-box performance acceptable, or do regulations require [[Linear Models\|linear]] coefficients or [[SHAP]] value explanations? |
| **Training Cost**       | How expensive is it to retrain when [[Train and Test#Train-Test Distribution Shift (Data Drift)]]                                     |




