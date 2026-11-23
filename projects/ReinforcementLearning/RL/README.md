# Reinforcement Learning: Multi-Armed Bandits & Q-Learning Pong

A reinforcement learning research and evaluation suite implementing exploration-exploitation strategies for stochastic multi-armed bandits and tabular Q-learning control for the classic Pong arcade environment.

---

## 1. Multi-Armed Bandit Exploration Strategies (`bandit/`)

### Mathematical Formulation
The multi-armed bandit problem models sequential decision-making under uncertainty, balancing the trade-off between exploring unmeasured actions and exploiting known high-payoff choices:

$$Q_t(a) = \frac{\sum_{i=1}^{t-1} R_i \cdot \mathbb{I}(A_i = a)}{\sum_{i=1}^{t-1} \mathbb{I}(A_i = a)}$$

### Algorithmic Features
* **Adaptive $\epsilon$-Greedy Policy:** Balances random exploratory arm pulls with greedy exploitation of max-expected-value arms, regulated by an exponential exploration decay schedule ($\epsilon \leftarrow \epsilon \cdot \lambda$).
* **Non-Stationary Environment Adaptation:** Handles dynamic reward distribution shifts across sequential simulation episodes without resetting action-value memories, maintaining sensitivity to environment transitions.
* **Empirical Benchmarking:** Evaluated against baseline stochastic bandits across 20 sequential simulation trials ($500 \pm 500$ pulls each), consistently surpassing the baseline cumulative reward by $>35\%$ in benchmark tests.

---

## 2. Q-Learning Control for Atari Pong (`pong/`)

### System Architecture
An autonomous agent trained via model-free Temporal Difference (TD) reinforcement learning to control paddle locomotion in a 2D Pong physics simulation:

* **State Discretization & Dimensionality Reduction:** Continuous game telemetry (paddle vertical coordinates, ball position $(x, y)$, and velocity directional vectors) is transformed and discretized into compact indexable state representations, mitigating state-space explosion.
* **Bellman Optimality Updates:** The action-value function is iteratively updated using the off-policy Temporal Difference error:

$$Q(s, a) \leftarrow Q(s, a) + \alpha \left[ r + \gamma \max_{a'} Q(s', a') - Q(s, a) \right]$$

* **Hyperparameter Configuration:**
  * Learning rate ($\alpha = 0.1$)
  * Discount factor ($\gamma = 1.0$) for delayed goal evaluation
  * Exploration schedule with minimum floor ($\epsilon_0 = 0.7$, $\epsilon_{\min} = 0.01$, decay $\lambda = 0.9$)
* **Action Space:** Discrete motor actions corresponding to paddle movement: Up, Down, and Hold.
