---
tags:
  - EDA
  - statistics
---
A visual tool for [[Exploratory Data Analysis Phases|Exploratory Data Analysis]] which provides smooth density estimate (via [[Kernel Density Estimation]]) over a continuous variable.

Use after [[histogram]] when you want smooth shape. Bandwidth = analogue of bin width.

Unlike with [[Histogram]], raw counts matter less with KDE plot. Instead, KDE provides visually better comparison across multiple groups. 

![[KDE Plot-1789919693347.webp]]

## Watch for

Boundary bias: KDE bleeds past real limits (e.g. extends below 0 for age). Use bounded kernels for constrained variables.

# 2D KDE

This plot places a smooth 2D [[Normal Distribution|Gaussian]] kernel over every data point and sums them to create a smooth surface, often visualized as a heat map or contour lines.

This plot works well when analyzing joint continuous distribution (density function) of two variables. 

![[KDE Plot-1789969145868.webp|502x502]]

**Use a 2D KDE Plot** when you want to emphasize underlying continuous distribution shapes, mode clusters, and probability contours rather than discrete sample counts (for discrete sample counts use [[Hexbin Plot]]).
## Key Parameters

As discussed in [[Kernel Density Estimation]], the most important parameter is bandwidth $h$ for both the regular and 2D KDE plot.

