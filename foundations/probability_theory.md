---
layout: default
title: Probability theory
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Probability theory

## Baye's theorem

$$P(A \mid B) = \frac{P(B \mid A) P(A)}{P(B)}$$

$$\textbf{posterior} \propto \textbf{likelihood} \times \textbf{prior}$$

| Term | Name | Description |
| :--- | :--- | :--- |
| $$P(A \mid B)$$ | **Posterior** | Probability of hypothesis $$A$$ given evidence $$B$$ |
| $$P(B \mid A)$$ | **Likelihood** | Probability of evidence $$B$$ given hypothesis $$A$$ |
| $$P(A)$$ | **Prior** | Initial probability of hypothesis $$A$$ |
| $$P(B)$$ | **Evidence** | Total probability of the evidence $$B$$ |

## Bernoulli distribution

The Bernoulli distribution is the simplest discrete probability distribution, representing a single trial with two possible outcomes (success or failure).

$$\begin{align}
f(k; p) &= \begin{cases} p & \text{if } k = 1 \\ 1-p & \text{if } k = 0 \end{cases} \\\\[6pt]
&= p^k (1-p)^{1-k} \quad k \in \{0,1\}
\end{align}$$



## Binomial distribution

The binomial distribution describes the number of successes in a fixed number of independent Bernoulli trials.

$$\displaystyle P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k}$$

with

$$\displaystyle \binom{n}{k} = \frac{n!}{k!(n - k)!}$$

## Gaussian distribution

$$\mathcal{N}(x \mid \mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x-\mu)^2}{2\sigma^2} \right)$$
