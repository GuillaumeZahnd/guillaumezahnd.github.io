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

- $$y_i : $$ Ground truth label for class $$i$$, with value $$1$$ for the correct class and $$0$$ otherwise (one-hot encoding).
- $$\hat{y}_i : $$ Predicted probability for class $$i$$ (usually corresponding to the softmax output).
- $$n : $$ Total number of classes.

## Root mean square error (RMSE)

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$$

- $$y_i : $$ Ground truth value for sample $$i$$.
- $$\hat{y}_i : $$ Predicted value for sample $$i$$.
- $$n : $$ Total number of samples.

## Softmax

$$\sigma(\mathbf{z})_i = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}$$

> [!CAUTION]
> - Risk of overflow: if $$z_i$$ is large ($$>88$$ in float32), then $$e^{z_i}$$ exceeds the numerical precision and returns $$\infty$$. Both the numerator and denominator would be $$\infty$$, and the softmax function would return `NaN`.
> - Risk of underflow: if $$z_i$$ is small ($$<-103$$ in float32), then $$e^z_i$$ rounds down to $$0.0$$. If all input are very small, the denominator becomes zero, thereby leading to a division-by-zero. The softmax function would return `NaN`.

## Stable softmax

$$\begin{align}
\sigma(\mathbf{z})_i &= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \\[6pt]
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \cdot \frac{e^{-M}}{e^{-M}} \quad \text{with }M=max_i(z_i) \\[6pt]
&= \frac{e^{z_i-M}}{\sum_{j=1}^{n} e^{z_j-M}} \\[6pt]
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \quad \text{with }\mathbf{x} = \mathbf{z} - M \\[6pt]
&= \sigma(\mathbf{x})_i
\end{align}$$

> [!NOTE]
> - Overflow is fully prevented: all values are constrained between $$0$$ and $$1$$, the numerator is always $$\leq 1$$ and the denominator is always $$\geq 1$$, therefore the result cannot be $$\infty$$.

> [!WARNING]
> - Underflow is partially handled: the denominator is always $$\geq 1$$ (avoiding division-by-zero), but the numerator can still underflow to $$0$$ if it is much smaller than the maximum value.

## Log-Sum-Exp trick

$$\begin{align}
log\Big(\sigma(\mathbf{z})_i\Big) &= log\left(\frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}\right) \\[6pt]
&=log(e^{z_i}) - log\left(\sum_{j=1}^{n} e^{z_j}\right) \\[6pt]
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M + M}\right) \quad \text{with }M=max_i(z_i) \\[6pt]
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M} \cdot e^M\right) \\[6pt]
&=z_i - M - log\left(\sum_{j=1}^{n} e^{z_j - M}\right)
\end{align}$$

## Regularization

Regularization is a technique used to prevent overfitting by adding a penalty term to the model's loss function. This penalty discourages the optimization algorithm from assigning excessively large values to the coefficients. Regularization can be seen as trading off a small amount of training accuracy in exchange for better generalization to unseen data.

### L1 Regularization (Lasso)

$$J(w) = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^{m} |w_j|$$

- $$\lambda : $$ Regularization parameter.
- $$w_j : $$ Model weight for parameter $$j$$.
- $$m : $$ Number of parameters.

### L2 Regularization (Ridge, equivalent to weight decay)

$$J(w) = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^{m} w_j^2$$

- $$\lambda : $$ Regularization parameter.
- $$w_j : $$ Model weight for parameter $$j$$.
- $$m : $$ Number of parameters.


