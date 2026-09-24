---
tags:
  - ML
---
Encoding categorical variables converts non-numeric data (like text labels or categories) into numerical representations that machine learning algorithms can process.

## Ordinal Encoding

Assigns each category a distinct integer based on its natural, logical order.

- **How it works:** Maps ordered labels directly to ordered numbers (e.g., `['Low', 'Medium', 'High']` $\rightarrow$ `[0, 1, 2]`).
- **Best used for:** **Ordinal features** where order carries intrinsic meaning (e.g., education level, customer satisfaction ratings, T-shirt sizes).
- **Pros & Cons:** Compact memory footprint, but introduces artificial linear relationships if applied to non-ordered (nominal) data. For [[Tree-Based Algorithms]] it does not matter so this type of encoding is safe for them.

## One-Hot Encoding (OHE)

Creates a new binary ($0$ or $1$) indicator column for each unique category level.

- **How it works:** A category column with $N$ levels is split into $N$ separate columns. For any given row, only the matching column gets a value of `1`, while all others are `0`.
- **Best used for:** **Nominal features** (no natural order) with **low cardinality** (few unique values, typically $< 15$). Common examples: gender, country code, payment method.
- **Pros & Cons:** Completely avoids imposing false numerical order. However, high-cardinality features cause the **curse of dimensionality** (massive, sparse feature matrices).
- **Dummy Variable Trap:** Linear models can suffer from multicollinearity if all $N$ columns are included. To prevent this, drop one column ($N-1$ columns total) using `drop='first'`.

## Target Encoding (Mean Encoding)

Replaces each category value with the mean of the target variable for that category.

- **How it works:** For a binary target $Y \in \{0, 1\}$, a category value like `"City: Seattle"` is replaced by the average rate of $Y=1$ across all rows where `City == 'Seattle'`.
- **Best used for:** **High-cardinality nominal features** (e.g., zip codes, product IDs, user IDs) in supervised learning problems.
- **Pros & Cons:** Extremely compact (keeps feature count at 1 column) and often improves tree model performance. However, it carries a severe risk of **data leakage** and **overfitting**.
- **Mitigation:** Always calculate target encoding within cross-validation folds and apply smoothing/[[regularization]] (blending the category mean with the global target mean). 

## Frequency / Count Encoding

Replaces each category value with its total count or relative frequency in the dataset.

- **How it works:** If `"Brand: Toyota"` appears $1,200$ times in a $10,000$-row dataset, it is replaced by $1200$ (count) or $0.12$ (frequency).
- **Best used for:** High-cardinality nominal features where the popularity/frequency of an item correlates with the target.
- **Pros & Cons:** Simple, fast, and does not leak target information. Weakness: Two completely different categories with similar frequencies will get identical values.

## Binary Encoding

Combines ordinal encoding with binary digits to create a compact representations of nominal data.

- **How it works:**
    1. Categories are converted to ordinal integers ($1, 2, 3, \dots, N$).
    2. Integers are converted into binary code (e.g., $5 \rightarrow 101_2$).
    3. Binary digits are split into separate columns.
- **Best used for:** Medium-to-high cardinality nominal features when you want to avoid both OHE dimensionality explosion and target encoding leakage.
- **Pros & Cons:** Encodes $N$ categories into only $\lceil\log_2(N)\rceil$ columns (e.g., $100$ categories require only $7$ columns instead of $100$). Reduces interpretability slightly.

## Selection Strategy

| **Encoding Method** | **Data Type** | **Cardinality** | **Best Algorithms**                                                                | **Key Risk / Caution**                                |
| ------------------- | ------------- | --------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------- |
| **Ordinal**         | Ordinal       | Low to High     | [[Tree-Based Algorithms]]                                                          | Imposes false order if data is nominal                |
| **One-Hot**         | Nominal       | Low ($< 15$)    | [[Linear Models]], [[Support Vector Machine\|SVM]], [[Neural Network\|NN]]s, Trees | Matrix explosion on high cardinality                  |
| **Target**          | Nominal       | High ($> 15$)   | [[Tree-Based Algorithms]] (XGBoost, LightGBM)                                      | High risk of data leakage / overfitting               |
| **Frequency**       | Nominal       | Medium to High  | Any algorithm                                                                      | Collision when different classes have equal frequency |
| **Binary**          | Nominal       | Medium to High  | [[Linear Models]], [[Neural Network\|NN]]s                                         | Loss of direct feature interpretability               |

## How to Handle Unknown Categories

Per [[Train and Test]] framework there might appear new categories at predict time in either test of validation sets. In this case all unknown categories could be assigned to "unknown". 