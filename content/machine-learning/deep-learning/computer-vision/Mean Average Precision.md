---
tags:
  - ML/computer-vision
aliases:
  - mAP
---
**Mean Average Precision (mAP)** is the ultimate gold-standard evaluation metric for object detection models.

While [[classification]] models are easily evaluated using simple metrics like [[Classification Metrics#Accuracy]], object detection is much harder. A model must not only guess the correct class (e.g., _dog_), but it must also draw a precise bounding box around it. mAP combines **localization accuracy** and **classification correctness** into a single, comprehensive score ranging from 0.0 to 1.0 (or 0% to 100%).
## The Building Blocks of mAP

To understand how mAP is calculated, you have to trace how a model's predictions are evaluated step-by-step:
### Defining Correctness with [[Intersection over Union|IoU]]

A prediction is counted as a **True Positive (TP)** only if:

- The predicted class label is correct.
- The **Intersection over Union (IoU)** between the predicted bounding box and the ground-truth box meets or exceeds a specific threshold (e.g., $\text{IoU} \ge 0.5$).
- If the box is misaligned or misplaced, it counts as a **False Positive (FP)**. Any real object the model failed to detect counts as a **False Negative (FN)**.
### Precision and Recall

By adjusting the model's confidence threshold, you shift how many boxes it outputs, creating a trade-off:

- [[Classification Metrics#Precision]]: Out of all the bounding boxes the model _predicted_, what percentage were actually correct?
-  [[Classification Metrics#Recall (Sensitivity / True Positive Rate)]]: Out of all the actual objects present in the images, what percentage did the model successfully _find_?

### Average Precision (AP) per Class

As you vary the confidence threshold, you can plot **Precision against Recall** on a curve. The **Average Precision (AP)** is mathematically calculated as the [[Precision-Recall AUC]] for a _single_ object class (like _cars_ or _pedestrians_). A model that maintains high precision even as recall approaches 1.0 will have an AP close to 1.0.

### Mean Average Precision (mAP)

An object detector rarely detects just one class of object; it usually handles dozens (e.g., COCO has 80 classes). **Mean Average Precision (mAP)** is simply the average of the AP scores calculated across all individual classes:

$$\text{mAP} = \frac{1}{N} \sum_{i=1}^{N} \text{AP}_i$$

_(where $N$ is the total number of classes)._

## The Two Major Standards: VOC vs COCO

Depending on the benchmark dataset you use, mAP is calculated using different stringency levels:

- **mAP@0.5 (Pascal VOC Style):** This is a more lenient standard. A bounding box is considered correct as long as its IoU with the ground truth is $\ge 0.5$ (50% overlap).
- **mAP@0.5:0.95 (COCO Style):** This is the modern, rigorous standard used by the MS COCO dataset. It calculates the mAP across **10 different IoU thresholds**—starting from 0.5 up to 0.95 with a step size of 0.05—and then averages them all together. A model with a high COCO mAP isn't just finding objects; it is drawing razor-tight bounding boxes around them.