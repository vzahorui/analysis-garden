---
tags:
  - ML
aliases:
  - Reproducibility
---
How to make a [[Machine Learning Pipeline]] run give the same scores and models when repeated. This is achieved by controlling every source of randomness that feeds [[Train and Test]], fitting, and [[Model Selection]].

# Cross-Validation Splits

[[Train and Test#What is Cross-Validation?|Cross-validation]] draws which rows land in which fold. Shuffle-based schemes (ordinary $K$-fold, ShuffleSplit, stratified folds after a shuffle) depend on a Random Number Generator (RNG). Fix and record that seed (or pass a seeded splitter) so the same fold membership is reused across models and hyperparameter trials. Otherwise you are comparing algorithms on different held-out slices, not the same evaluation design from [[Train and Test]] split.

Also export indices corresponding to train/validation/test datasets. When the full pipelines runs anew, simply read the indiced rather that do the splitting again - that is the safest route because something could have changed in the algorithms producing random numbers. 

# Sampling of Observations and Features

Many learners redraw data inside fitting:

* **Bootstrap / bagging**: resample observations with replacement for each base learner (as in [[Random Forest]]).
* **Feature subsampling**: random subsets of columns per tree, per split, or per boosting round.
* **Mini-batches and data order**: SGD-style optimizers ([[Gradient Descent]]) shuffle rows each epoch unless told not to.

Each of these streams needs a controlled RNG (or a single shared random state on the estimator) if you want bit-stable or at least fold-stable comparisons.

# Other Randomized Pipeline Behavior

Typical extras that move scores if left free:

* Dummy / stratified random baselines ([[Dummy Estimators]]).
* Stochastic regularizers and dropout in [[Neural Network|neural nets]].
* Random search / Bayesian optimization proposals in [[Model Selection]].
* Parallelism and non-deterministic Basic Linear Algebra Subprograms (BLAS) ops: same seeds can still differ across hardware or thread counts; note the environment when claiming exact match.

Prefer one documented seed policy for the whole experiment (splitters + estimators + search) over ad-hoc per-call seeds.

# Random Forest: Shared Random State

For [[Random Forest]], set a **single random state** on the ensemble (the forest’s RNG). That stream drives bootstrap draws and feature subsampling for every tree in sequence, so tree-to-tree learning stays properly random relative to each other while the forest as a whole is reproducible.

Avoid assigning a **fixed predetermined seed to each tree** up front. That can force an artificial, hand-picked randomness pattern instead of letting the forest’s RNG generate the bagging and feature draws as one coherent process. 
