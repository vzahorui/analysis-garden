---
tags:
  - EDA
---
A 2D [[histogram]] that tessellates the plotting area into a regular grid of hexagons and counts how many observations fall into each cell. Cell color maps to observation count.

> [!Note] **Why Hexagons over Squares?**
> -  Hexagons have six neighbors instead of four, and all adjacent centers are equidistant. This reduces visual artifacts (directional bias) and creates a more natural representation of spatial density compared to standard square grid heatmaps.

It serves as an altertative to [[Scatter Plot]] when the number of observations is too big to be informative as a scatter plot.

![[Hexbin Plot-1789968070825.webp]]

## Key Parameters

As with [[Histogram]], the key parameter here is bin width.