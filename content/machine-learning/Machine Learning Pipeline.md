---
tags:
  - ML
---
Predictive specialization of [[Analysis Workflow Phases]], entered from [[Analytical Framing]] on the modeling path. Keep runs comparable with [[Pipeline Reproducibility]].

# Steps

1. [[Validation Strategy]]: how evaluation is possible (full / partial / no labels).
2. Choose your primary [[Choice of a Scoring Metric|optimization metric]] when the validation branch allows it (e.g., F1-score, ROC-AUC, RMSE), plus business-facing guardrail metrics (e.g., inference latency, memory footprint).
3. [[Modelling Decision]] (interpretability / accuracy / speed). See [[Model Families Comparison]].
4. Create [[Train and Test]] datasets consistent with the validation design. Verify there is no [[Train and Test#Train-Test Distribution Shift (Data Drift)]]
5. [[Exploratory Data Analysis Phases|Exploratory Data Analysis]] over train data only.
6. Using a `Pipeline` do [[Feature Preprocessing]] using train data only (excluding validation set, as it will only reuse the learned transformtaion from the trained set). Later the same Pipeline will also contain the actual model over the preprocessed data.
7. Building a set of models ([[Dummy Estimators|baseline]] + enhanced models).
8. [[Model Selection]]

## Other References

* [[Pipeline Reproducibility]]
