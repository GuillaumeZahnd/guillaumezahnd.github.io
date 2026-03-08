---
layout: default
title: Mechine learning
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Mechine learning

## Categorical cross-entropy loss

$$\mathcal{L} = -\sum_{i=1}^{n} y_i \log(\hat{y}_i)$$

- $$y_i$$: Ground truth label for class $$i$$, with value $$1$$ for the correct class and $$0$$ otherwise (one-hot encoding).
- $$\hat{y}_i$$: Predicted probability for class $$i$$ (usually corresponding to the softmax output).
- $$n$$: Total number of classes.

## Root mean square error (RMSE)

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$$

- $$y_i$$: Ground truth value for sample $$i$$.
- $$\hat{y}_i$$: Predicted value for sample $$i$$.
- $$n$$: Total number of samples.

## Softmax

$$\sigma(\mathbf{z})_i = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}$$

> [!CAUTION]
> Risk of overflow
> Risk of underflow

## Stable softmax

$$\begin{align}
\sigma(\mathbf{z})_i &= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \\
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \cdot \frac{e^{-M}}{e^{-M}} \quad \text{with }M=max_i(z_i) \\
&= \frac{e^{z_i-M}}{\sum_{j=1}^{n} e^{z_j-M}} \\
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \quad \text{with }\mathbf{x} = \mathbf{z} - M \\
&= \sigma(\mathbf{x})_i
\end{align}$$

> [!NOTE]
> Overflow is fully prevented: all values are constrained between $$0$$ and $$1$$, the numerator is always $$\leq 1$$ and the denominator is always $$\geq 1$$, therefore the result cannot be $$\infty$$.

> [!WARNING]
> Underflow is partially handled: the denominator is always $$\geq 1$$ (avoiding division-by-zero), but the numerator can still underflow to $$0$$ if it is much smaller than the maximum value.

## Log-Sum-Exp trick

$$\begin{align}
log\Big(\sigma(\mathbf{z})_i\Big) &= log\left(\frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}\right) \\
&=log(e^{z_i}) - log\left(\sum_{j=1}^{n} e^{z_j}\right) \\
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M + M}\right) \quad \text{with }M=max_i(z_i) \\
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M} \cdot e^M\right) \\
&=z_i - M - log\left(\sum_{j=1}^{n} e^{z_j - M}\right) \\
\end{align}$$
