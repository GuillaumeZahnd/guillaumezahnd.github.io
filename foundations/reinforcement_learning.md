---
layout: default
title: Reinforcement learning
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Reinforcement learning

## Bellman expectation equation

The Bellman expectation equation is used to calculate the value of a state under a fixed policy.

$$V^\pi(s) = \sum_{a \in \mathcal{A}} \Bigg( \pi(a|s) \sum_{s' \in \mathcal{S}, r \in \mathcal{R}} P(s', r \mid s, a) \Big(r + \gamma V^\pi(s')\Big) \Bigg)$$

- $$V^\pi(s) : $$ Value of state $$s$$ under policy $$\pi$$.
- $$a : $$ Action.
- $$\mathcal{A} : $$ Set of all possible actions.
- $$s$$, $$s' : $$ States.
- $$\mathcal{S} : $$ Set of all possible states.
- $$r : $$ Reward.
- $$\mathcal{R} : $$ Set of all possible rewards.
- $$P(s', r \mid s, a) : $$ Probability to transition from state $$s'$$ with reward $$r$$ from state $$s$$ with action $$a$$.
- $$\gamma : $$ Discount factor.

## Bellman optimality equation

The Bellman optimality equation is used to calculate the maximum possible value of a state under the optimal policy.

$$V^\ast(s) = \max_{a \in \mathcal{A}} \sum_{s', r} p(s', r \mid s, a) \Big(r + \gamma V^\ast(s')\Big)$$
