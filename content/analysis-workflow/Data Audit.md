---
tags:
  - analysis
  - workflow
---
![[Data Audit.excalidraw.svg]]

In scope of the null audit it may be useful to build a heatmap of missing values across the columns.

When performing duplicate check pay attention not only on the exact duplicates but also on the partial duplicates. For example the same record could be logged several times with different timestamps. Or the same record could be logged twice: one with corrupted or missing values and another with normal values.

If data is incompatible with [[Problem Framing]] then its worth revisiting it.