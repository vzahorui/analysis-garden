---
tags:
  - statistics
aliases:
  - normal
  - Gaussian
  - normality
  - normally distributed
---
The **normal distribution** (often called the **bell curve** or **Gaussian distribution**) is a continuous [[Probability Distributions|Probability Distribution]] that is symmetric around its mean. It describes how values of a variable are distributed when most observations cluster around a central average, with extreme values tapering off equally in both directions.

## Key Characteristics

- **Symmetry:** The left and right halves are mirror images.
- **Central Tendency:** The mean, median, and mode are all equal and located at the center of the peak.
- **Parameters:** It is defined entirely by two parameters:
    - **Mean ($\mu$):** Determines the center or location of the peak.
    - **Standard Deviation ($\sigma$):** Determines the spread or width of the curve. Higher $\sigma$ makes the curve flatter and wider.

![[Normal Distribution-1790490561741.webp]]

## The Empirical Rule (68–95–99.7/6 sigma Rule)

In any normal distribution, data falls predictable distances from the mean based on standard deviations:

| **Range**         | **Enclosed Probability / Data** |
| ----------------- | ------------------------------- |
| $\mu \pm 1\sigma$ | **~68.27%** of all values       |
| $\mu \pm 2\sigma$ | **~95.45%** of all values       |
| $\mu \pm 3\sigma$ | **~99.73%** of all values       |

## Probability Density Function (PDF)

The mathematical formula for the normal distribution's curve is:

$$f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{x - \mu}{\sigma}\right)^2}$$
- **$x$:** The variable value.
- **$\mu$:** The population mean.
- **$\sigma$:** The standard deviation.
- **$e$:** Euler's number ($\approx 2.71828$).
- **$\pi$:** Pi ($\approx 3.14159$).
## The Standard Normal Distribution ($Z$-distribution)

A **standard normal distribution** is a specific case where the mean $\mu = 0$ and the standard deviation $\sigma = 1$.

Any normal variable $X$ can be converted into a standard normal variable $Z$ using the $Z$-score formula:

$$Z = \frac{X - \mu}{\sigma}$$

The $Z$-score measures how many standard deviations an observation $X$ lies above or below the mean.

![[Normal Distribution-1790490520033.webp]]