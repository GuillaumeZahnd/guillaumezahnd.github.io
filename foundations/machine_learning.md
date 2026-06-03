---
layout: default
title: Machine learning
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Machine learning

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
\sigma(\mathbf{z})_i &= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \\\\[6pt]
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \cdot \frac{e^{-M}}{e^{-M}} \quad \text{with }M=max_i(z_i) \\\\[6pt]
&= \frac{e^{z_i-M}}{\sum_{j=1}^{n} e^{z_j-M}} \\\\[6pt]
&= \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}} \quad \text{with }\mathbf{x} = \mathbf{z} - M \\\\[6pt]
&= \sigma(\mathbf{x})_i
\end{align}$$

{: .note-title }
> Note
>
> Overflow is fully prevented: all values are constrained between $$0$$ and $$1$$, the numerator is always $$\leq 1$$ and the denominator is always $$\geq 1$$, therefore the result cannot be $$\infty$$.

{: .warning-title }
> Warning
>
> Underflow is partially handled: the denominator is always $$\geq 1$$ (avoiding division-by-zero), but the numerator can still underflow to $$0$$ if it is much smaller than the maximum value.

## Log-Sum-Exp trick

$$\begin{align}
log\Big(\sigma(\mathbf{z})_i\Big) &= log\left(\frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}\right) \\\\[6pt]
&=log(e^{z_i}) - log\left(\sum_{j=1}^{n} e^{z_j}\right) \\\\[6pt]
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M + M}\right) \quad \text{with }M=max_i(z_i) \\\\[6pt]
&=z_i - log\left(\sum_{j=1}^{n} e^{z_j - M} \cdot e^M\right) \\\\[6pt]
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

## Optimizers

The fundamental difference between Stochastic Gradient Descent (SGD) and Adam (Adaptive Moment Estimation) lies in how they scale the step size. SGD applies a uniform learning rate to all parameters, whereas Adam calculates distinct, adaptive learning rates for every single weight by tracking historical gradients.

### Notations

- $$\theta_t$$:  Model parameters (weights) at step $$t$$
- $$g_t = \nabla J(\theta_t)$$: Gradient of the loss function $$J$$ with respect to $$\theta_t$$
- $$\eta$$: Learning rate
- $$\gamma$$ or $$\beta$$: Decay coefficients for moving averages

| Metric | SGD | SGD with momentum | Adam |
| :--- | :--- | :--- | :--- |
| **Weight update formula** | $$\theta_{t+1} = \theta_t - \eta g_t$$ | $$v_t = \gamma v_{t-1} + g_t$$<br>$$\theta_{t+1} = \theta_t - \eta v_t$$ | $$\theta_{t+1} = \theta_t - \displaystyle\frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$ |
| **Learning rate** | Constant for all parameters | Constant scaled by velocity | Adaptive for each parameter |
| **Convergence** | Slow; prone to oscillation | Accelerated along consistent directions | Fast initial phase, especially in sparse settings |
| **Local minima** | Easily trapped | Momentum helps navigate saddles and flat regions | Adaptive step scaling helps navigate ravines and ill-conditioned curvature |
| **Memory** | Low (no auxiliary state, $$O(1)$$) | Medium (stores $$v_t$$, $$O(N)$$ extra memory) | High (stores $$m_t$$ and $$v_t$$, $$O(2N)$$ extra memory) |
| **Tuning sensitivity** | High (highly sensitive to $$\eta$$) | Medium | Low (default hyperparameters usually robust) |

### Mathematical formulations

#### SGD with Momentum

Momentum addresses the oscillations of standard SGD in ravines by adding a fraction $$\gamma$$ of the previous update vector to the current step:

$$v_t = \gamma v_{t-1} + g_t$$

$$\theta_{t+1} = \theta_t - \eta v_t$$

#### Adam

Adam computes adaptive learning rates by tracking both the exponentially decaying average of past gradients (first moment, $$m_t$$) and exponentially decaying average of past squared gradients (second uncentered moment, $$v_t$$):

$$m_t = \beta_1 m_{t-1} + (1 - \beta_1)g_t$$

$$v_t = \beta_2 v_{t-1} + (1 - \beta_2)g_t^2$$

Because $$m_t$$ and $$v_t$$ are typically initialized as vectors of zeros, they are biased toward zero, especially during the initial time steps. To counteract this, Adam applies bias-corrected estimators:

$$\hat{m}_t = \displaystyle\frac{m_t}{1 - \beta_1^t}$$

$$\hat{v}_t = \displaystyle\frac{v_t}{1 - \beta_2^t}$$

The final update equation scales the step size inversely proportional to the root mean square of past gradients:

$$\theta_{t+1} = \theta_t - \displaystyle\frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$

Note: $$\epsilon$$ is a small smoothing term (typically $$10^{-8}$$) to prevent division by zero. Typical default hyperparameters are $$\beta_1 = 0.9$$ and $$\beta_2 = 0.999$$.

### When to use Adam over SGD

- **Deploy Adam when:** You are prototyping a new, unproven architecture, working with sparse data, dealing with complex multimodal loss landscapes (e.g., Transformers, GANs), or have strict constraints on hyperparameter tuning time.
- **Deploy SGD with Momentum when:** You are optimizing a standard architecture (e.g., ResNets in computer vision) for maximum generalization performance. Adam's aggressive scaling can cause the optimizer to overshoot narrow, robust minima, leading to poorer generalization on the test set compared to a well-tuned SGD routine.

## Manifold

A manifold is a topological space that locally resembles a Euclidean space (that is, every point has a neighborhood that is homeomorphic to an open subset of $$\mathbb{R}^n$$), even if its global structure is much more complex.

{: .note-title }
> Note
>
> - A manifold is the formal way of describing shapes that are "locally flat." For instance, taking the perspective of an ant walking on the surface of a balloon, the world looks like a flat 2D plane, even though the balloon is actually a 3D sphere.
> - Other examples of manifolds include a circle, which locally resembles a line, and the surface of a $$n$$-sphere, which locally resembles a $$n-1$$ hyperplane.
> - Manifold is a critical assumption in Machine Learning to handle high dimensional data. Many datasets lie near a lower-dimensional manifold embedded in a high-dimensional space, meaning the intrinsic structure of the data has fewer degrees of freedom than the ambient dimension.

## Likelihood and log-likelihood

### Likelihood

The likelihood function $$L(\theta)$$ represents the plausibility of a fixed set of observed data across different variations of the model parameters $$\theta$$. The goal of Maximum Likelihood Estimation (MLE) is to find the specific value $$\hat{\theta}$$ that maximizes $$L(\theta)$$.

$$L(\theta) = \prod_{i=1}^{n} P(x_i \mid \theta)$$

### Log-likelihood

The log-likelihood $$\ell(\theta)$$ is the natural logarithm of the likelihood function. Because the logarithm is a monotonically increasing function, the value $$\hat{\theta}$$ that maximizes the likelihood also maximizes the log-likelihood.

$$\ell(\theta) = \log(L(\theta)) = \sum_{i=1}^{n} \log(P(x_i \mid \theta))$$

### Why use log-likelihood instead of likelihood?

1. **Mathematical simplicity:** The logarithm converts products into sums, which are easier to differentiate.
2. **Numerical stability:** Probabilities are numbers between 0 and 1. Multiplying thousands of such small values may result in arithmetic underflow. The logarithm turn these values into manageable negative numbers.
3. **Exponential family:** Several common distributions (Gaussian, Bernoulli, Poisson) contain an exponential term. The logarithm cancels out the exponential, leaving a linear or quadratic expression that is easy to solve.
