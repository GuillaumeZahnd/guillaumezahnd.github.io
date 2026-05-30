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
| **Environment** | -- | The environment constitutes the external system or dynamic "world" with which the agent interacts. It encompasses all physical or logical constraints, transition dynamics, and reward mechanisms outside the agent's direct control. Upon receiving an action, the environment transitions to a new state and emits a corresponding feedback signal. |
|  **State** | $$s_t \in \mathcal{S}$$ | Comprehensive representation of the environment's configuration at a specific time step $$t$$. If the environment is only partially observable, the agent receives an observation $$o_t$$ of the underlying state $$s_t$$. The state serves as the information basis for the agent's decision-making process. |
| **Action** | $$a_t \in \mathcal{A}(s)$$ | Discrete or continuous maneuvers available to the agent at any given state. The selection of an action is governed by the agent’s policy $$\pi$$. The action results in the transition to state $$s_{t+1}$$ and the receipt of reward $$r_{t+1}$$. |
| **Reward** | $$R_t$$ | Scalar feedback signal provided by the environment to quantify the immediate success of an action. |
| **Return** | $$G_t$$ | Discounted sum of all future rewards for a given trajectory:<br><br>$$G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \dots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1} = R_{t+1} + \gamma G_{t+1}$$<br><br>where $$\gamma \in (0, 1]$$ is the discount factor. |
| **Policy** | $$\pi(a \mid s)$$ | Agent's strategy for mapping states to actions. Formally, it defines the probability distribution of taking action $$a$$ given state $$s$$:<br><br>$$\pi(a \mid s) := P(a_t = a \mid s_t = s)$$<br><br>If the policy is deterministic instead of stochastic, then $$\pi(s)=a$$. |

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
- $$P(s', r \mid s, a) : $$ Probability for the environment to transition from state $$s'$$ with reward $$r$$ from state $$s$$ with action $$a$$.
- $$\gamma : $$ Discount factor.

## Bellman optimality equation

The Bellman optimality equation is used to calculate the maximum possible value of a state under the optimal policy.

$$V^\ast(s) = \max_{a \in \mathcal{A}} \sum_{s' \in \mathcal{S}, r \in \mathcal{R}} p(s', r \mid s, a) \Big(r + \gamma V^\ast(s')\Big)$$

## Optimal policy

The optimal policy $$\pi^\ast$$ is the strategy that achieves the optimal value function $$V^\ast$$.

$$\displaystyle \pi^\ast(s) = \arg\max_{a \in \mathcal{A}} \sum_{s' \in \mathcal{S}, r \in \mathcal{R}} p(s', r \mid s, a) \Big(r + \gamma V^\ast(s')\Big)$$

{: .note-title }
> Note
>
> There may be multiple optimal policies if different actions lead to the same maximum reward.

## Regret

Regret is a metric that quantifies the cumulative expected difference between the actual reward $$r_t$$ earned by an agent using its own policy and the maximal reward $$r_t^\ast$$ that could have been earned by following the optimal policy.

$$\text{Regret}(T) = \mathbb{E} \left[ \sum_{t=1}^{T} r_t^\ast - r_t \right]$$

{: .note-title }
> Note
>
> Regret is useful to measure the performance loss caused by the exploration-exploitation tradeoff.

## Model-based vs. model-free learning

{: .note-title }
> Note
>
> The core distinction between model-based and model-free RL lies in whether the agent utilizes an explicit internal representation of the environment's transition dynamics and reward functions.

### Model-based learning

The agent first learns a model of the environment that predicts state transitions and rewards, then uses this model to plan future actions via simulation before executing them.

The model is learned by collecting real-world transition data (tuples of the current state, action taken, next state, and reward) as the agent interacts with the environment. This data is then used to train supervised learning algorithms (e.g., neural networks or transition tables) that map state-action pairs to their predicted next states and rewards.

$$\mathcal{M}(s, a) = \Big( P(s' \mid s, a), \, R(s, a) \Big)$$

### Model-free learning

The agent learns directly from trial-and-error experience, updating its value functions or policies based on observed transitions.

### Comparison

| | Model-based RL | Model-free RL |
| :--- | :--- | :--- |
|**Examples**| Chess Autonomous vehicle trajectory planning, Industrial chemical process control | Maze navigation, Atari video games, Quadrupedal locomotion over rough terrain |
| **Core mechanism** | Learn model $$\rightarrow$$ Plan $$\rightarrow$$ Act | Act $$\rightarrow$$ Learn from experience |
| **Sample efficiency** | High (requires few real-world interactions) | Low (requires extensive trial-and-error) |
| **Computational overhead** | High (intensive simulation) | Low (direct value/policy updates) |
| **Robustness** | Moderate, can be vulnerable to modeling errors | High, capable to handle to highly complex, non-linear, or stochastic dynamics that are difficult to model accurately |
| **Primary Risk** | Asymptotic suboptimality due to model bias, potentially leading to high compounding errors | High variance and poor performance in early exploration |

## On-policy vs. off-policy learning

{: .note-title }
> Note
>
> The core distinction between on-policy vs. off-policy learning lies in how the underlying algorithm utilizes data and depends on the relationship between two specific policies:

- **Behavior policy ($$\mu$$):** The policy used by the agent to interact with the environment and select actions.
- **Target policy ($$\pi$$):** The policy that the agent is actively evaluating, refining, and optimizing.

### On-policy learning

In on-policy algorithms, the target policy and the behavior policy are identical ($$\pi=\mu$$). The agent learns exclusively from data generated by its current strategy, meaning it "learns by doing." Every policy update changes the data distribution, forcing the agent to constantly collect new experience using its newly updated policy.

- **Characteristics:** Highly stable but sample-inefficient. Because the agent must account for its own exploration mechanisms (e.g., stochastic choices), it optimizes for safety and online performance during training.
- **Example Algorithm:** SARSA (State-Action-Reward-State-Action).

### Off-policy learning

In off-policy algorithms, the target policy and the behavior policy are distinct ($$\pi \neq \mu$$). The agent evaluates and optimizes a target policy (often a deterministic, greedy policy) while interacting with the environment using a separate, exploratory behavior policy. It essentially "learns by watching."

- **Characteristics:** Highly sample-efficient but potentially unstable. Because the updates are decoupled from the agent's actual behavior, the algorithm can leverage historical data, human demonstrations, or experience generated by completely different agents.
- **Example Algorithm:** Q-Learning.

### Comparison

| | On-policy learning | Off-policy learning |
| :--- | :--- | :--- |
| **Primary application** | Online real-world systems: Physical robotics or critical machinery where exploration steps must be safe and account for real-time risk | Simulators & legacy datasets: Autonomous driving fleets or recommendation engines that must learn from human logs or historical data |
| **Policy relationship** | Target policy equals behavior policy ($$\pi = \mu$$) | Target policy differs from behavior policy ($$\pi \neq \mu$$) |
| **Core objective** | Optimize the value of the *current* exploratory policy, forcing the experience to reflect the current strategy | Optimize the value of the *target* (usually optimal) policy, regardless of how the agent is currently exploring |
| **Data efficiency** | Low: Data must be discarded after a policy update | High: Can reuse historical data via a replay buffer, parallel runs, human input |
| **Exploration risk** | Low: Avoids high-risk states by accounting for exploratory randomness | High: Maximizes theoretical returns, aims for optimal performance, but ignores the cost of real-world exploration and prone to catastrophic failures |
| **Stability** | High: Stable and reliable convergence guarantees | Low: Prone to divergence (the "Deadly Triad" when combined with function approximation) |
