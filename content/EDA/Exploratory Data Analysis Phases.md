---
tags:
  - analysis
  - EDA
aliases:
  - EDA
  - Exploratory Data Analysis
---
This should be the first step in data analysis after the data is clean enough and pre-processed.

# Phase 1: Univariate analysis

![[Univariate EDA.excalidraw.svg]]

## Histograms

Meant to reveal modality (uni/bi/multi), skewness, floor/ceiling effects, impossible values.

When building histograms be extra careful when selecting the bin size. Bin width is a tuning parameter, not a fact. Start with Sturjes, then tune. Always try at least 3 different bin counts before concluding.

If the data is heavily skewed it makes sense to apply logarithmic transformation to the data. 

#todo make the chart of log-transformed data 
#todo add section on sturjes rule (# Scott's rule, https://en.wikipedia.org/wiki/Freedman%E2%80%93Diaconis_rule)
