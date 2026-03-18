---
layout: default
title: Information theory
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Information theory

## Entropy

Entropy measures the average "uncertainty" or "surprise" associated with a set of possible outcomes. Developed by Claude Shannon in 1948, it quantifies how much information is produced by a source of data.

The entropy $$H(X)\geq0$$ for a discrete random variable $$X$$ is defined as:

$$\displaystyle H(X) = -\sum_{x \in \mathcal{X}} P(x) \log_b P(x)$$

- $$P(x) : $$ Probability that the random variable $$X$$ takes a specific value $$x$$ from the set $$\mathcal{X}$$.
-  $$\mathcal{X} : $$ Set of all possible outcomes.
- $$b : $$ Logarithm base (in base 2, the entropy is expressed in bits).

## Cross-entropy

Cross-entropy measures the average quantity of information required to identify an event when using a coding scheme optimized for distribution $$Q$$ (the model) rather than using the true distribution $$P$$ (the ground truth).

The cross-entropy $$H(P, Q)\geq0$$ between two discrete probability distributions $$P$$ and $$Q$$ is defined as:

$$\begin{align}
\displaystyle H(P, Q) &= -\sum_{x \in \mathcal{X}} P(x) \log_b Q(x)\\\\[6pt]
& \geq H(P)
\end{align}$$

- $$P(x) : $$ True probability distribution.
- $$Q(x) : $$ Estimated probability distribution.
- $$H(P) : $$ Entropy of the true probability distribution. 
- $$\mathcal{X} : $$ Set of all possible outcomes.
- $$b : $$ Logarithm base (in base 2, the entropy is expressed in bits).

## Kullback-Leibler divergence

The Kullback-Leibler (KL) divergence (also known as *relative entropy*), measures how one much an estimated probability distribution $$Q$$ differs from the true probability distribution $$P$$. 

The KL divergence $$D_{KL}(P \mid Q)\geq0$$ between two discrete probability distributions $$P$$ and $$Q$$ is defined as:

$$\begin{align}
\displaystyle D_{KL}(P \mid Q) &= \sum_{x \in \mathcal{X}} P(x) \log \left( \frac{P(x)}{Q(x)} \right) \\\\[6pt]
&= H(P, Q) - H(P)
\end{align}$$

- $$P(x) : $$ True probability distribution.
- $$Q(x) : $$ Estimated probability distribution.
- $$H(P) : $$ Entropy of the true probability distribution. 
- $$H(P, Q) : $$ Cross-entropy between the estimated and the true probability distributions. 
- $$\mathcal{X} : $$ Set of all possible outcomes.
- $$b : $$ Logarithm base (in base 2, the entropy is expressed in bits).

> [!NOTE]
> - **Information theory:** The KL divergence corresponds to the "extra bits" that are wasted to encode samples from $$P$$ using a code optimized for $$Q$$ instead of the true distribution $$P$$.
> - **Bayesian inference:** The KL divergenve represents the information gain (or surprise) achieved when updating beliefs from a prior distribution $$Q$$ to a posterior distribution $$P$$ after observing data.
> - **Asymmetry:** $$D_{KL}(P \mid Q) \neq D_{KL}(Q \mid P)$$. Because the KL divergence 
violates the symmetry and triangle inequality axioms, it is a *divergence* and not a *distance* or *metric*.
> - **Non-negativity:** $$D_{KL}(P \mid Q) \geq 0$$. The KL divergence equals zero if and only if $$P = Q$$. 

