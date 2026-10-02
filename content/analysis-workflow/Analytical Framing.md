---
tags:
  - analysis
  - workflow
---
This is strongly dependent on the available data.

![[Analytical Framing.excalidraw.svg|697]]

[[Data Audit]] already cleared readiness. From here, fork:

1. **Simple analysis** (descriptive, or diagnostics without a predictive build) → [[Exploratory Data Analysis Phases|EDA]].
2. **Modeling path** (predictive, or diagnostics that need a model) → [[Machine Learning Pipeline]] (constraint → family, train/test, train-only EDA, selection, [[Validation Strategy|validation]], and the rest live there).

If question type shifts mid-analysis -> reset the scope in [[Problem Framing]].
