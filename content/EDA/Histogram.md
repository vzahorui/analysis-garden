---
tags:
  - EDA
---
A visual tool for [[Exploratory Data Analysis Phases#Phase 1 Univariate analysis]]. 

Meant to reveal modality (uni/bi/multi), skewness, floor/ceiling effects, impossible values.

When building histograms be extra careful when selecting the bin size. Bin width is a tuning parameter, not a fact. Start with Sturjes, then tune. Always try at least 3 different bin counts before concluding.

If the data is heavily skewed it makes sense to apply logarithmic transformation to the data. 

#todo make the chart of log-transformed data 
#todo add section on sturjes rule (# Scott's rule, https://en.wikipedia.org/wiki/Freedman%E2%80%93Diaconis_rule)

# Selecting number of  bins

For quick exploratory analysis use by default Freedman–Diaconis rule. It relies on the **Interquartile Range ($\text{IQR}$)** rather than the standard deviation, making it resilient against outliers, heavy-tailed data, and extreme values.

The optimal bin width $h$ is calculated as:

$$h = 2 \cdot \frac{\text{IQR}(X)}{\sqrt[3]{n}}$$
Where:
- $\text{IQR}(X) = Q_3 - Q_1$ is the Interquartile Range of the dataset $X$ (the range containing the middle 50% of data).
- $n$ is the total number of observations (sample size).

Once $h$ is computed, the total number of bins $k$ across a data range $[\min(X), \max(X)]$ is given by:
$$k = \left\lceil \frac{\max(X) - \min(X)}{h} \right\rceil$$
## Conceptual Foundations of Freedman–Diaconis rule

It relies on [[Asymptotic Normal Theory]] and [[Kernel Density Estimation]]. The aim is to minimize the difference between the true underlying probability density function $f(x)$ and the histogram estimate $\hat{f}(x)$.

