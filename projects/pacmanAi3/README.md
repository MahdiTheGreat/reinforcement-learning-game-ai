# Markov Decision Processes & Reinforcement Learning Agents

A dynamic programming and model-free reinforcement learning framework implementing value iteration, tabular Q-learning, and feature-based approximate Q-learning across discrete Gridworld, robotic crawling, and multi-agent game environments.

---

## 1. Dynamic Programming & MDP Solvers (`valueIterationAgents.py`)

A Markov Decision Process (MDP) is formalized by the 5-tuple $(S, A, T, R, \gamma)$, where transition probabilities $T(s, a, s')$ and rewards $R(s, a, s')$ are fully known.

### Value Iteration Implementations
* **Batch Value Iteration (`ValueIterationAgent`):** Solves the Bellman Optimality Equations offline by iteratively computing state values across synchronous passes:

$$V_{k+1}(s) \leftarrow \max_{a \in A} \sum_{s' \in S} T(s, a, s') \left[ R(s, a, s') + \gamma V_k(s') \right]$$

* **Asynchronous In-Place Value Iteration (`AsynchronousValueIterationAgent`):** Updates states in-place sequentially, immediately feeding new value estimates into successor calculations within the same iteration cycle.
* **Prioritized Sweeping Value Iteration (`PrioritizedSweepingValueIterationAgent`):** Accelerates convergence by maintaining a max-priority queue keyed on Bellman error magnitude:

$$\text{Error}(s) = \left| V(s) - \max_{a} \sum_{s'} T(s, a, s') \left[ R(s, a, s') + \gamma V(s') \right] \right|$$

States with the highest error are popped and updated first, and significant error deltas are systematically pushed backward to upstream predecessor states.

---

## 2. Model-Free Temporal Difference Reinforcement Learning (`qlearningAgents.py`)

In environments where transition probabilities and reward distributions are unknown, the agent learns optimal action-value functions directly from sample trajectories $(s, a, r, s')$.

### Tabular Q-Learning (`QLearningAgent`)
* **Off-Policy TD Update Rule:**

$$Q(s, a) \leftarrow Q(s, a) + \alpha \left( r + \gamma \max_{a'} Q(s', a') - Q(s, a) \right)$$

* **Exploration Policy:** $\epsilon$-greedy action selection selecting random exploratory actions with probability $\epsilon$ and greedy action $\arg\max_a Q(s, a)$ with probability $1 - \epsilon$.

---

## 3. Approximate Q-Learning with Linear Function Approximation (`ApproximateQAgent`)

For environments with combinatorial state spaces where tabular representations are infeasible, the action-value function is modeled as a linear combination of basis features:

$$Q(s, a) = \sum_{i=1}^n w_i \cdot f_i(s, a)$$

### Gradient Descent Weight Update
Upon observing transition $(s, a, r, s')$, weights $w_i$ are updated online along the gradient of the mean-squared Bellman error:

$$\text{difference} = \left[ r + \gamma \max_{a'} Q(s', a') \right] - Q(s, a)$$

$$w_i \leftarrow w_i + \alpha \cdot \text{difference} \cdot f_i(s, a)$$

### Feature Engineering (`featureExtractors.py`)
* **Identity Extractor:** Maps $(s, a)$ pairs directly to orthogonal indicator features.
* **Coordinate Extractor:** Encodes relative spatial agent and goal offsets.
* **Domain Feature Extractor (`SimpleExtractor`):**
  * Ghost 1-step hazard indicator (active ghost within collision radius).
  * Reciprocal distance to the nearest food pellet.
  * Food consumption indicator (immediate transition reward).

---

## Benchmark Environments

* **Gridworld (`gridworld.py`):** Configurable transition noise, terminal reward states, and discount factors ($\gamma$) to study risk sensitivity (e.g., navigating near cliffs vs. taking safe long paths).
* **Crawler Robot (`crawler.py`):** Physical 2-joint robotic arm learning forward locomotion through continuous motor coordination and ground contact dynamics via tabular Q-learning.
* **Game Agent (`pacman.py`):** High-dimensional maze environment where Approximate Q-learning generalizes across unseen board configurations without needing to memorize specific layout coordinates.
