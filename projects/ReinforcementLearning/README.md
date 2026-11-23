# Reinforcement Learning & Game Intelligence

A modular framework containing reinforcement learning algorithms and adversarial board game agents implemented in Python and Java.

---

## Subsystems

### 1. Adversarial Othello / Reversi Game Engine (`Othello/`)
* **Adversarial Search:** Implements the Minimax game-tree search algorithm augmented with **Alpha-Beta Pruning** to minimize tree expansion while preserving search depth.
* **Dual-Language Architecture:** Provides complete game board abstractions, move generation, and legal move validation in both **Python** and **Java**.
* **Evaluation Functions:**
  * Disc count and board parity evaluation.
  * Strategic positional heuristics weighting corner dominance, edge control, and mobility frontiers.
* **Benchmarking Harness:** Shell automation scripts (`othello.sh`, `othellostart`) executing timed competitive matches against baseline naive agents and external tournament engines.

### 2. Stochastic Bandits & Temporal Difference Q-Learning (`RL/`)
* **Multi-Armed Bandits (`RL/bandit/`):** Adaptive exploration algorithms with exponential $\epsilon$-decay solving stochastic reward optimization problems under stationary and non-stationary conditions.
* **Autonomous Pong Agent (`RL/pong/`):** Model-free Temporal Difference Q-learning agent learning reactive paddle control against continuous physics environments via spatial state discretization.
