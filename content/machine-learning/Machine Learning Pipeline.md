---
tags:
  - ML
---
# Steps

1.  Create [[Train and Test]] datasets. Verify there is no [[Train and Test#Train-Test Distribution Shift (Data Drift)]]
2. [[Exploratory Data Analysis Phases|Exploratory Data Analysis]] over train data only. 
3. Using a `Pipeline` do [[Preprocessing Numerical Features]]  using train data only (excluding validation set, as it will only reuse the learned transformtaion from the trained set). Later the same Pipeline will also contain the actual model over the preprocessed data.


