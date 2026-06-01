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

## Expectation under $$Q$$

Integrating a function weighted by $$q(z)$$ over the latent space is equivalent to taking an expectation under $$q(z)$$, a substitution that converts integrals into a form amenable to approximation and optimization.

$$\int_{\mathcal{Z}} q(z) \frac{p(z)}{q(z)}~dz = \mathbb{E}_{q(z)}\left[\frac{p(z)}{q(z)}\right]$$

## Kullback-Leibler divergence

The Kullback-Leibler (KL) divergence (also known as *relative entropy*), measures how one much an estimated probability distribution $$Q$$ differs from the true probability distribution $$P$$. 

The KL divergence $$D_{\mathrm{KL}}(P \| Q)\geq0$$ between two discrete probability distributions $$P$$ and $$Q$$ is defined as:

$$\begin{align}
\displaystyle D_{\mathrm{KL}}(P \| Q) &:= \sum_{x \in \mathcal{X}} P(x) \log \left( \frac{P(x)}{Q(x)} \right) \\\\[6pt]
&= H(P, Q) - H(P)
\end{align}$$

- $$P(x) : $$ True probability distribution.
- $$Q(x) : $$ Estimated probability distribution.
- $$H(P) : $$ Entropy of the true probability distribution. 
- $$H(P, Q) : $$ Cross-entropy between the estimated and the true probability distributions. 
- $$\mathcal{X} : $$ Set of all possible outcomes.
- $$b : $$ Logarithm base (in base 2, the entropy is expressed in bits).

{: .note-title }
> Note
>
> - **Information theory:** The KL divergence corresponds to the "extra bits" that are wasted to encode samples from $$P$$ using a code optimized for $$Q$$ instead of the true distribution $$P$$.
> - **Bayesian inference:** The KL divergenve represents the information gain (or surprise) achieved when updating beliefs from a prior distribution $$Q$$ to a posterior distribution $$P$$ after observing data.
> - **Asymmetry:** $$D_{\mathrm{KL}}(P \mid Q) \neq D_{\mathrm{KL}}(Q \mid P)$$. Because the KL divergence 
violates the symmetry and triangle inequality axioms, it is a *divergence* and not a *distance* or *metric*.
> - **Non-negativity:** $$D_{\mathrm{KL}}(P \mid Q) \geq 0$$. The KL divergence equals zero if and only if $$P = Q$$.

## Evidence lower bound (ELBO)

### Starting posulate: intractable evidence

We want to maximize $$p(x \mid M)$$ because it represents the probability that our model $$M$$ would generate the data $$x$$ we observed. To determine the optimal parameters of the model, we want to maximize the log-likelihood of the true evidence $$\log p(x)$$. However, this requires integrating over all possible latent variables $$z$$:

$$\log p(x) = \log \int p(x, z)~dz = \log \int p(x|z) p(z)~dz$$

For complex high-dimensional models, this integral is intractable.

### Paradigm change and Jensen's inequality

Instead of asking *"how do I compute* $$log p(x)$$*?"*, ELBO asks *"can I find a lower bound that's easy to optimize?"*. The key insight is to introduce an auxiliary distribution $$q(z|x)$$.

$$\begin{aligned}
\log p(x) 
&= \log \int p(x, z) dz \\
&= \log \int q(z|x) \frac{p(x, z)}{q(z|x)} dz \\
&= \log \mathbb{E}_{q(z|x)} \left[ \frac{p(x, z)}{q(z|x)} \right]  \quad \text{(Expectation under~} q \text{)}\\
&\geq \mathbb{E}_{q(z|x)} \left[ \log \frac{p(x, z)}{q(z|x)} \right] \quad \text{(Jensen's Inequality, since log is concave, $\log \mathbb{E}[\cdot] \geq \mathbb{E}[\log \cdot]$)} \\
\end{aligned}$$

{: .note-title }
> Note
>
> The ELBO is defined as
> $$\text{ELBO} := \mathbb{E}_{q(z|x)} \left[ \log \frac{p(x, z)}{q(z|x)} \right]$$

### Relationship with the KL divergence

$$\begin{aligned}
D_{\mathrm{KL}}\left(q(z|x) \| p(z|x)\right) 
&= \int q(z|x) \log \frac{q(z|x)}{p(z|x)}~dz \\
&= \mathbb{E}_{q(z|x)}\left[\log \frac{q(z|x)}{p(z|x)}\right] \\
&= \mathbb{E}_{q(z|x)}\left[\log \frac{q(z|x) p(x)}{p(x,z)}\right] \quad \text{(Applying Bayes' rule)}\\
&= \mathbb{E}_{q(z|x)}\left[\log \frac{q(z|x)}{p(x,z)}\right] + \mathbb{E}_{q(z|x)}\left[\log p(x)\right] \\
&= -\text{ELBO} + \log p(x)
\end{aligned}$$

{: .important-title }
> Important
>
> $$\log p(x) = \text{ELBO} + D_{\mathrm{KL}}\left(q(z|x) \| p(z|x)\right)$$
>
> Since $$D_{\mathrm{KL}} \geq 0$$ the ELBO is a tractable lower bound on the true log-evidence $$\log p(x)$$. Therefore, maximizing the ELBO simultaneously tightens the lower bound and pushes our approximation $$q(z|x)$$ toward the true posterior $$p(z∣x)$$, without ever needing to compute the latter directly.
