---
tags:
  - ML
aliases:
  - loss
---
## Summary Comparison
| Concept               | Primary Purpose                    | Differentiable? | Aggregation        |
| :-------------------- | :--------------------------------- | :-------------- | :----------------- |
| **Loss Function**     | Optimization during training       | Required        | Per-sample / Batch |
| **Evaluation Metric** | Performance reporting & comparison | Not Required    | Dataset-level      |

## Key Differences
- **Optimization vs. Evaluation:** The optimizer (e.g., Adam, SGD) updates model parameters using the **Loss Function**.  Model utility is evaluated using an **Evaluation Metric**.
- **Mathematical Constraints:** Loss functions must be continuous and smooth to allow gradient computation. Evaluation metrics (like Accuracy or F1-Score) can be non-differentiable or discontinuous.

## Typical Dual-Usage
Some measures serve both roles depending on context:
- [[Mean Squared Error]] serves as both a loss function and an evaluation metric.
- [[Cross-Entropy]] is used as a loss during training, but reported as log-loss during evaluation.