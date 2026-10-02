---
tags:
  - ML
---
Early gate on the [[Machine Learning Pipeline]]: given label availability, decide how evaluation works:  standard metrics, mixed (labeled subset + expert review), or expert and logic checks.

![[Validation Strategy.excalidraw.svg]]

That choice feeds [[Choice of a Scoring Metric]] (when metrics apply) and the split design in [[Train and Test]]. 

[[Model Selection]] later executes the plan. If results fail sanity, return to [[Data Audit]] or earlier Pipeline steps (including [[Modelling Decision]]).
