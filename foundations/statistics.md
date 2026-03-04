---
layout: default
title: Statistics
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Statistics

## Power analysis

The validity of a statistical test is governed by five interdependent parameters (see Table below). 

| Parameter | Notation | Description | Controllability |
| :--- | :--- | :--- | :--- |
| **Minimum detectable effect** | $$\delta=\mu_1 - \mu_2$$ | Magnitude of the expected difference. Larger effects are easier to observe. | Fixed. The target is set by research goals, but the underlying effect magnitude is fixed. | 
| **Sample size** | $$n$$ | Number of observations. | High, within budget. This is the primary lever for controlling power. |
| **Variance** | $$\sigma^2$$ | Noise in the data. | Low, via experimental control and measurement precision. |
| **Significance level** | $$\alpha$$ | False positive rate (specificity). | High, specified upfront. Corresponds to the p-value threshold. |
| **Statistical power** | $$1 - \beta$$ | True positive rate (sensitivity). | High, specified upfront. |

Mathematically, these variables exist in a closed system where fixing any four uniquely determines the fifth (see Equation below).

$$\displaystyle n = \frac{2 \sigma^2}{\delta^2} \Big( Z_{1-\alpha/2} + Z_{1-\beta} \Big)^2$$


