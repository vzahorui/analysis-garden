---
tags:
  - ML
---
Choose after [[Validation Strategy]] when that gate allows metric-based evaluation. The scoring metric choise is largely dicated by a business (or other external) requirement.

Otherwise the scoring function must be closely in-line with measuring the difference between prediction and observation.

* Metrics used for predictions are usually the same as the ones used for optimization ([[Loss vs Metric]] functions). 
* Metrics used for making decisions are usually the ones used in [[Classification]] based on assigning the final label to a target. See [[Classification Metrics]].

