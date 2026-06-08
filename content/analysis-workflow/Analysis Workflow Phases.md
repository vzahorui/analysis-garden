---
tags:
  - analysis
  - workflow
aliases:
  - Analysis Workflow
---
What I do when I encounter any type of problem for analysis.

# Phases

1. [[Problem Framing]]
2. [[Data Audit]]
3. [[Analytical Framing]]
4. [[Modelling Decision]]
5. [[Validation Strategy]]
6. [[Communication]]


Each phase ends with a checkpoint — I pause and verify before moving forward. It might be possible that I need to return to an earlier phase. In practice, the most common non-linear paths are:

- **Phase 2 → Phase 1 loop:** I discover the data that exists is fundamentally incompatible with the outcome I defined. The problem needs to be reframed before any analysis makes sense.
- **Phase 5 → Phase 2 or Phase 4 loop:** Validation reveals something wrong at a lower level — either the data was dirtier than audited, or the model family was the wrong choice for the structure of the problem.
- **Phase 3 → Phase 1 implicit tension:** The analytical question type (descriptive, predictive, etc.) sometimes shifts once I see the data. When that happens, I need the stakeholder agreement from Phase 1 updated before continuing — otherwise I am answering a different question than anyone asked.

# Apply at every phase

* Document decisions and their rationale as you go.
* Check for representational bias in data and outputs.
* Flag scope creep as soon as it appears.
* End with a stakeholder checkpoint.