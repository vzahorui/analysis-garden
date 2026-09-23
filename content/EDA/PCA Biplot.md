---
tags:
  - EDA
  - statistics
---
A **PCA Biplot** is a 2D graph that overlay two sets of information from a dataset onto the same [[Principal Component Analysis|principal components]] axes: the transformed **observations** (data points) and the original **variables** (features).

In [[Exploratory Data Analysis Phases|Exploratory Data Analysis]], it allows you to visualize sample clusters while simultaneously seeing which specific variables drive those patterns.

![[PCA Biplot-1790019315099.webp|492x511]]

## Key Components of a Biplot

A biplot standardly uses **PC1** as the horizontal axis and **PC2** as the vertical axis (representing the two directions of highest variance in the dataset).
### 1. Scores (Data Points)

- **What they are:** Represented as dots or markers. These are the projections of the original observations onto the principal components.
- **How to read:**
    - Points that are **close together** have similar multivariate profiles across the features.
    - Points far from the origin along PC1 or PC2 are extreme cases driving high variance along those components.
### 2. Loadings (Variable Vectors)

- **What they are:** Represented as arrows originating from $(0,0)$. Each arrow represents one original feature from the dataset.
- **How to read:**
    - **Vector Length:** Indicates how well that variable is explained by the two displayed components. A longer vector means higher variance captured in PC1 and PC2.
    - **Vector Direction:** Shows how strongly the variable contributes to PC1 vs. PC2.

## Practical Value in EDA

- **Cluster Profiling:** If observations group into separate clusters, look at which variable vectors point toward each cluster to immediately see _why_ they differ.

- **Feature Redundancy:** Clusters of parallel vectors indicate redundant features that measure similar underlying signals.
    
- **Outlier Diagnosis:** Points isolated in the direction of a long vector highlight anomalies driven by that specific variable.
## Watch for

[[Principal Component Analysis|PCA]] is a linear method. Non-linear structure (spirals, clusters with varying density) won't resolve well.

![[PCA Biplot-1789969887587.webp]]