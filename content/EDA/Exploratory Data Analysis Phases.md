---
tags:
  - analysis
  - EDA
aliases:
  - EDA
  - Exploratory Data Analysis
---
This should be the first step in data analysis after the data is clean enough and pre-processed.
* no duplicates
* NULL values are understood.

# Phase 1: Univariate analysis

![[Univariate EDA.excalidraw.svg]]

This will reveal the general shape of dimensions and main categories.

See more detailed notes:
* [[Box Plot]]
* [[Histogram]]
* [[KDE Plot]]
* [[Q-Q Plot]]
# Phase 2: Anomaly and Shift Checks

## Outliers flagging

1. Using z-score for approximatelly [[Normal Distribution|normally distributed]] variables.
2. Using IQR fences for skewed distributions (the way [[Box Plot]] does it).
## Distribution Shift Checks

1. Compare feature distributions between [[Train and Test]].
2. Compare feature distributions across time windows. Features whose distribution differs between periods - the ones most likely to degrade model performance.
## Target variable leakage

Check if any feature shows near-perfect predictive correlation with the target variable. It might be derived from it after the fact, or measured concurrently with it.
# Phase 3: Bivariate analysis
![[Bivariate EDA.excalidraw.svg]]

This is will reveal relationship between variables and will allow comparisons across dimensions.

See more detailed notes:
* [[Scatter Plot]]
* [[Pearson Correlation]]
* [[Spearman Correlation]]
* [[Kendall Correlation]]
* [[Hexbin Plot]]
* [[KDE Plot#2D KDE]]

# Phase 4: Multivariate Analysis

After the bivariate analysis, this will allow having a comparison of strengths of all pairwise relationships at once, and asssess their relevance. 
![[Multivariate EDA.excalidraw.svg]]
See more detailed notes:
* [[HDBSCAN]]
* [[GLOSH]]
* [[PCA Biplot]]
* [[Parallel Coordinates Plot]]
# Phase 5: Synthesis & hypothesis log

## Hypothesis Register

Write down every 'I think X because I saw Y' as a falsifiable statement. 
## Feature Shortlist

Prune dimensionality before modeling for [[Machine Learning Concepts|Machine Learning]]. 
## Data Quality Report

Summary of nulls, outliers, type issues, and corrective actions taken.