---
layout: default
title: Reinforcement learning
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Reinforcement learning


| Name | Notation | Description |
| :--- | :--- | :--- |
| **Agent** | -- | Autonomous entity or learner that interprets environment feedback to make decisions. Its primary function is to map perceived states $$s$$ to specific actions while optimizing a behavioral policy $$\pi$$. The ultimate objective is to select actions that maximize the return $$G_t$$, which is the discounted sum of rewards over a specific horizon. |
|  **State** | $$s_t \in \mathcal{S}$$ | Comprehensive representation of the environment's configuration at a specific time step $$t$$. If the environment is only partially observable, the agent receives an observation $$o_t$$ of the underlying state $$s_t$$. The state serves as the information basis for the agent's decision-making process. |
| **Action** | $$a_t \in \mathcal{A}(s)$$ | Discrete or continuous maneuvers available to the agent at any given state. The selection of an action is governed by the agent’s policy $$\pi$$. The action results in the transition to state $$s_{t+1}$$ and the receipt of reward $$r_{t+1}$$. |
| **Environment** | -- | The environment constitutes the external system or dynamic "world" with which the agent interacts. It encompasses all physical or logical constraints, transition dynamics, and reward mechanisms outside the agent's direct control. Upon receiving an action, the environment transitions to a new state and emits a corresponding feedback signal. |
| **Reward** | $$R_t$$ | Scalar feedback signal provided by the environment to quantify the immediate success of an action. |
| **Return** | $$G_t$$ | Discounted sum of all future rewards for a given trajectory:<br><br>$$G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \dots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1} = R_{t+1} + \gamma G_{t+1}$$<br><br>where $$\gamma \in (0, 1]$$ is the discount factor. |
| **Policy** | $$\pi(a \mid s)$$ | Agent's strategy for mapping states to actions. Formally, it defines the probability distribution of taking action $$a$$ given state $$s$$:<br><br>$$\pi(a \mid s) := P(a_t = a \mid s_t = s)$$. |

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
