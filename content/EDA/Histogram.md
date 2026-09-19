---
tags:
  - EDA
  - statistics
---
A visual tool for [[Exploratory Data Analysis Phases#Phase 1 Univariate analysis]]. 

Meant to reveal modality (uni/bi/multi), skewness, floor/ceiling effects, impossible values.

If the data is heavily skewed it makes sense to apply logarithmic transformation to the data. 
![[Histogram-1789836023100.webp]]

# Selecting number of  bins

For quick exploratory analysis use by default Freedman–Diaconis rule. It relies on the **Interquartile Range ($\text{IQR}$)** rather than the standard deviation, making it resilient against outliers, heavy-tailed data, and extreme values.

Try experimenting with different bin sizes before making a conclusion.
## Freedman–Diaconis rule

The optimal bin width $h$ is calculated as:

$$h = 2 \cdot \frac{\text{IQR}(X)}{\sqrt[3]{n}}$$
Where:
- $\text{IQR}(X) = Q_3 - Q_1$ is the Interquartile Range of the dataset $X$ (the range containing the middle 50% of data).
- $n$ is the total number of observations (sample size).

Once $h$ is computed, the total number of bins $k$ across a data range $[\min(X), \max(X)]$ is given by:
$$k = \left\lceil \frac{\max(X) - \min(X)}{h} \right\rceil$$