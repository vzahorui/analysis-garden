---
tags:
  - ML
---
Model selection is the process of choosing the optimal machine learning algorithm and configuration (hyperparameters) for a given dataset and problem statement. It aims to find a model that minimizes generalization error on unseen data by navigating the [[Bias and Variance]]. 
## The Core Objective: Generalization

Every model selection decision trades off capacity against stability. Refer to [[Bias and Variance#Managing the Bias-Variance Tradeoff]] for the statistical mechanics.

## Validation Framework

Model selection requires an unbiased evaluation pipeline which is where [[Train and Test#What is Cross-Validation?|Cross-Validation]] (CV) comes in handy.
## The Selection Workflow

Baseline Model  ──►  Model Exploration ──► Hyperparameter Tuning ──►  Final Test Evaluation
### Step 1: Baseline
Start with a simple, highly interpretable model (e.g., Linear Regression or a decision tree) to establish an minimum acceptable performance benchmark.
### Step 2: Algorithm Screening
Create diverse models from different families which can be applied to a problem at hand:
* [[Linear Models]] / [[Regularization|Regularized]] Models (High Bias, Low Variance baseline)
* [[Tree-Based Algorithms]] ([[Random Forest]], XGBoost, LightGBM)
* [[Neural Network|Neural Networks]] / Specialized architectures
### Step 3: Hyperparameter Tuning
Once the candidate algorithms are identified, optimize their parameters using the most suited [[Objectives & Metrics|metrics]] (e.g., F1-score, RMSE, [[AUC]]):
* **Grid Search:** Exhaustive search over a fixed parameter grid.
* **Random Search:** Random sampling of parameter spaces; more efficient in high dimensions.
* **[[Bayesian Statistics|Bayesian]] Optimization:** Probabilistic search that uses prior trial evaluation history to sample optimal parameters.

The model complexity can also be tuned by looking at validation curve as in [[Bias and Variance#Managing the Bias-Variance Tradeoff]].

### Step 4: Final Model Selection

Compare the best model candidate in its own family across identical CV splits and select the best one.

If several model produce nearly identical results - select the simpler one (the one which is more interpretable and less computation demanding).

## Evaluation Criteria Beyond Raw Metrics

While optimization relies on specific performance [[Objectives & Metrics|metrics]], production model selection must also evaluate trade-offs in real-world constraints:

| Constraint              | Consideration                                                                                                                         |
| :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **Inference Latency**   | Does the model meet real-time requirements (e.g., single tree vs. 100-tree ensemble)?                                                 |
| **Model Size / Memory** | Can it run on edge devices or budget instances?                                                                                       |
| **Interpretability**    | Is black-box performance acceptable, or do regulations require [[Linear Models\|linear]] coefficients or [[SHAP]] value explanations? |
| **Training Cost**       | How expensive is it to retrain when [[Train and Test#Train-Test Distribution Shift (Data Drift)]]                                     |




