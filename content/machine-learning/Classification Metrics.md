---
tags:
  - ML/classification
---
# Binary Classification
## The Confusion Matrix

The foundation of binary [[classification]] metrics is the **Confusion Matrix**, which tracks actual versus predicted class labels across four outcomes:

- **True Positive (TP):** Model predicted Positive; Actual is Positive (Correct).
- **True Negative (TN):** Model predicted Negative; Actual is Negative (Correct).
- **False Positive (FP) — Type I Error:** Model predicted Positive; Actual is Negative (False Alarm).
- **False Negative (FN) — Type II Error:** Model predicted Negative; Actual is Positive (Missed Detection).

### Accuracy

The ratio of all correct predictions over total predictions:

$$\text{Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$$

- **When to use:** Only when classes are well-balanced and all error types carry equal cost.
- **The Trap:** If 99% of samples are class 0, a model that predicts 0 for everything achieves 99% accuracy while being useless.

### Precision

Out of everything the model predicted as Positive, how many were actually Positive?

$$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

- **Priority:** Minimizing **False Positives** (FP).
- **Example:** Spam filtering. Marking a critical work email as spam (FP) is far worse than letting an actual spam email into the inbox (FN). High precision ensures flagged items are genuine.

### Recall (Sensitivity / True Positive Rate)

Out of all actual Positive cases in the data, how many did the model correctly identify?

$$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

- **Priority:** Minimizing **False Negatives** (FN).
- **Example:** Cancer detection or fraudulent transaction screening. Missing a malignant tumor (FN) is dangerous, so you tolerate false alarms (FP) to catch every real case.

### F1-Score

The harmonic mean of Precision and Recall:

$$\text{F1} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}} = \frac{2 \cdot \text{TP}}{2 \cdot \text{TP} + \text{FP} + \text{FN}}$$

- **Why Harmonic Mean?** Unlike an arithmetic mean, the harmonic mean heavily penalizes extreme trade-offs. If Precision is 1.0 and Recall is 0.0, the arithmetic mean is 0.5, but the F1-score drops to 0.0.
- **When to use:** When you need a single metric that balances Precision and Recall, especially under class imbalance.

## Balancing Between Precision and Recall

* [[ROC Curve]] allows you to tune the threshold to balance between false positive rate and recall.
    * [[AUC]] as a derived metric from [[ROC Curve]] allows you to evaluate the model under every possible threshold value, and is an indicator of how good the model is (compared to others).
* [[Precision-Recall AUC]] as a better alternative of [[AUC]] for imbalanced data. 
# Handling Multiclass Evaluation: Macro vs Micro Averaging

In multiclass classification ($K > 2$), metrics like Precision, Recall, and F1 are computed for each individual class $k$. To summarize model performance into a single number, aggregation strategies are used.

### Macro Averaging

Calculates the metric independently for each class, then takes the unweighted arithmetic mean:

$$\text{Precision}_{\text{macro}} = \frac{1}{K} \sum_{k=1}^{K} \text{Precision}_k$$

$$\text{F1}_{\text{macro}} = \frac{1}{K} \sum_{k=1}^{K} \text{F1}_k$$

- **Key Property:** Treats all classes equally, regardless of support (the number of true instances per class).
- **When to use:** When performance on minority classes is just as critical as on majority classes (e.g., rare disease classification).

### Micro Averaging

Aggregates the global counts of TP, FP, and FN across all classes first, then computes the overall metric:

$$\text{Precision}_{\text{micro}} = \frac{\sum_{k=1}^{K} \text{TP}_k}{\sum_{k=1}^{K} \text{TP}_k + \sum_{k=1}^{K} \text{FP}_k}$$

- **Key Property:** Gives equal weight to every individual sample. Larger classes naturally dominate the result.
- **Note:** In single-label multiclass classification where every sample receives exactly one prediction, $\text{Micro Precision} = \text{Micro Recall} = \text{Micro F1} = \text{Accuracy}$.

### Summary Comparison

| **Metric**      | **Computation**                           | **Sensitivity to Class Imbalance**            | **Primary Use Case**                               |
| --------------- | ----------------------------------------- | --------------------------------------------- | -------------------------------------------------- |
| **F1-Macro**    | Average of per-class F1 scores            | **High:** Severe drop if minority class fails | Evaluating balanced performance across all classes |
| **F1-Micro**    | Global TP/FP/FN pooled calculation        | **Low:** Dominated by majority class          | Evaluating overall sample-level throughput         |
| **F1-Weighted** | Class F1 scores weighted by class support | **Medium:** Reflects actual data distribution | General benchmark when distribution matters        |

