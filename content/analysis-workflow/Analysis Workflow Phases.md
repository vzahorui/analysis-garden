---
tags:
  - workflow
aliases:
  - Analysis Workflow
---
What I do when I encounter any type of problem for analysis.

# Phases

1. [[Problem Framing]]
2. [[Data Audit]]
3. [[Analytical Framing]]
4. [[Communication]]


Each phase ends with a checkpoint: I pause and verify before moving forward. It might be possible that I need to return to an earlier phase. In practice, the most common non-linear paths are:

- **Phase 2 → Phase 1 loop:** I discover the data that exists is fundamentally incompatible with the outcome I defined. The problem needs to be reframed before any analysis makes sense.
- **Phase 3 → Phase 1 implicit tension:** The analytical question type (descriptive, predictive, etc.) sometimes shifts once I see the data. When that happens, I need the stakeholder agreement from Phase 1 updated before continuing, otherwise I am answering a different question than anyone asked.
- **Modeling path:** When Analytical Framing chooses predictive work, evaluation lives in the [[Machine Learning Pipeline]] ([[Validation Strategy]], [[Train and Test]], [[Model Selection]]). Failures there may still loop back to [[Data Audit]] or Phase 1.

# Apply at Every Phase

* Document decisions and their rationale as you go.
* Check for representational bias in data and outputs.
* Flag scope creep as soon as it appears.
* End with a stakeholder checkpoint.
