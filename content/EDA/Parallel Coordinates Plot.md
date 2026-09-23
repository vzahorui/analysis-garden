---
tags:
  - EDA
---
A **Parallel Coordinates Plot** is a data visualization technique used to analyze multivariate, high-dimensional numerical data (see [[Exploratory Data Analysis Phases#Phase 3 Multivariate Analysis]]).

Instead of arranging axes orthogonally (perpendicular to each other at 90 degrees, like in a standard Cartesian scatter plot), axes are placed **parallel to one another**—typically evenly spaced vertical or horizontal lines.

Each observation is a **polyline** that crosses those axes at its feature values. The shape of the line is the observation's multivariate profile.

![[Parallel Coordinates Plot-1790022736215.webp]]
## How to Read the Patterns

- **Clustering & Groups:** Lines that trace similar paths across axes form distinct visual bundles, indicating clusters or subpopulations in your data.
- **Correlations between Adjacent Axes:**
    - **Direct (Positive) Correlation:** Parallel or non-crossing lines between two adjacent axes indicate that high values on axis $A$ align with high values on axis $B$.
    - **Inverse (Negative) Correlation:** Lines crossing over each other in an $X$-shape indicate that high values on axis $A$ correspond to low values on axis $B$.
- **Outliers:** A line that strays completely away from main bundles or follows a starkly unique slope across axes clearly highlights an anomaly.

## Key Strengths

* __High Dimensionality__: Scales easily to 5, 10, or 20+ features simultaneously on a single 2D plot. On the contrary, [[PCA Biplot]] squeezes everything into a two-dimensional space.
* **Multivariate Trade-offs:** Excellent for spotting complex trade-offs (e.g., high performance vs. low fuel efficiency).
* Unlike [[PCA Biplot]] it can spot non-linear relationship.
## Limitations

* **Overplotting ("Hairball Effect"):** With thousands of observations, overlapping lines obscure patterns. Requires transparency, opacity adjustments, or sampling.
* **Axis Order Sensitivity:** Relationships are easiest to spot between _adjacent_ axes. Reordering the axes can reveal completely different relationships.
* **Scaling Nuance:** Variables on vastly different scales require normalization (e.g., min-max or z-score transformation) to avoid misleading slope interpretations.

