---
tags:
  - ML
aliases:
  - Dummy Estimator
---
A **dummy estimator** predicts from a trivial rule that ignores the features, e.g. always the training-set mean (regression), always the majority class, or stratified random guesses (classification).

In the [[Machine Learning Pipeline]], this is the first [[Model Selection|baseline]]: score it with the same [[Choice of a Scoring Metric|metric]] and [[Train and Test|validation]] design as every other model. Anything that cannot beat the dummy has not learned a useful signal yet.

Common strategies (sklearn-style):

* **Regression:** `mean`, `median`, `quantile`, or a constant.
* **Classification:** `most_frequent`, `stratified`, `uniform`, or a constant label.

Keep the dummy in the comparison set through screening: it anchors how much real models are actually buying you.
