---
tags:
  - ML
  - statistics
aliases:
  - linear combinations
  - linear combination
  - linear model
---
A **linear model** is a mathematical equation used to predict or explain an outcome based on a straight-line relationship between inputs and outputs.

In simple terms, it assumes that changing an input variable by a certain amount will always produce a proportional change in the target outcome.

# The Fundamental Equation

For a model predicting an outcome ($y$) based on a single input variable ($x$), the equation is:

$$y = \beta_0 + \beta_1 x + \varepsilon$$

- **$y$ (Dependent / Target Variable):** What you are trying to predict (e.g., house price, total revenue, test score).
- **$x$ (Independent / Feature Variable):** The input factor used to make the prediction (e.g., square footage, ad spend, hours studied).
- **$\beta_0$ (Intercept):** The baseline value of $y$ when $x = 0$.
- **$\beta_1$ (Slope / Coefficient):** The rate of change. It tells you how much $y$ increases or decreases for every 1-unit increase in $x$.
- **$\varepsilon$ (Error / Residual):** The gap between the actual observed value and what the straight line predicted (accounting for randomness and unmeasured factors). See [[Residual vs Error]].

# Multiple Linear Regression

In real-world applications, outcomes rarely depend on just one factor. A **Multiple Linear Model** expands the equation to handle multiple inputs simultaneously:

$$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_p x_p + \varepsilon$$

**Example:** Predicting annual house heating costs ($y$):

- $x_1$ = Square footage of the home ($\beta_1$ > 0: larger home increases cost)
- $x_2$ = Average winter temperature ($\beta_2$ < 0: warmer weather decreases cost)
- $x_3$ = Insulation thickness in inches ($\beta_3$ < 0: better insulation decreases cost)

# Key Assumptions

For a linear model to produce reliable and statistically sound results, four main assumptions must hold (often remembered by the acronym **LINE**):

1. **Linearity:** The relationship between the inputs and the mean outcome is truly linear.
2. **Independence:** The errors/observations are independent of one another (no time-series auto-correlation).
3. **Normality:** The errors ($\varepsilon$) are [[Normal Distribution|normally distributed]] around zero $\mathcal{N}(0, \sigma^2)$.
4. **Equal Variance (Homoscedasticity):** The spread/variance of the errors remains constant across all values of $x$.

# Strengths & Limitations

| **Strengths**                                                                                               | **Limitations**                                                                                                              |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **High Interpretability:** Coefficients directly show the exact impact of each input.                       | **Over-simplification:** Cannot capture complex, non-linear patterns (e.g., exponential growth) without feature engineering. |
| **Computationally Efficient:** Trains instantly even on massive datasets.                                   | **Sensitivity to Outliers:** Extreme data points can heavily skew the fitted line.                                           |
| **Clear Statistical Inference:** Provides [[confidence intervals]] and p-values for [[hypothesis testing]]. | **Multicollinearity Risks:** Highly correlated inputs can cause unstable coefficient estimates.                              |
# Prominent examples

* [[Linear Regression]]
* [[Logistic Regression]]