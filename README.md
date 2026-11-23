# Reinforcement Learning & Game Intelligence Monorepo

A unified engineering and research monorepo containing autonomous decision agents, reinforcement learning systems, adversarial game-playing engines, and state-space search algorithms. The repository integrates exact dynamic programming, model-free temporal difference control, linear value-function approximation, multi-agent minimax with alpha-beta pruning, stochastic multi-armed bandits, and robotic locomotion control, preserving complete Git commit histories across all projects.

---

## Engineering & Algorithmic Pillars

```
                     Reinforcement Learning & Game Intelligence
                                         │
    ┌────────────────────┬───────────────┴───────────────┬────────────────────┐
    ▼                    ▼                               ▼                    ▼
Heuristic Search   Adversarial Search           Markov Decision         Reinforcement
& Planning         & Game Theory                Processes (MDPs)        Learning (RL)
• DFS, BFS, UCS    • Minimax (1-vs-k)           • Value Iteration       • Multi-Armed Bandits
• A* & Greedy      • Alpha-Beta Pruning         • Asynchronous VI       • Tabular Q-Learning
• Admissible Heur. • Expectimax (Probabilistic) • Prioritized Sweeping  • Approx. Q-Learning
```

---

### 1. Heuristic Search & State-Space Pathfinding
* **[`projects/pacmanAi/`](projects/pacmanAi/)**:
  * Uninformed exploration architectures: Depth-First Search (DFS), Breadth-First Search (BFS), and Uniform Cost Search (UCS).
  * Informed heuristic search: A\* Search and Greedy Best-First Search with admissible and consistent heuristics ($f(n) = g(n) + h(n)$).
  * High-dimensional state space formulations: Multi-corner traversal (`CornersProblem`) and relaxed minimum spanning tree food clearing (`FoodSearchProblem`).

---

### 2. Adversarial Search & Multi-Agent Game Theory
* **[`projects/pacmanAi2/`](projects/pacmanAi2/)**:
  * Multi-agent zero-sum minimax game trees coordinating a single MAX agent against $k$ concurrent MIN ghost adversaries.
  * Alpha-Beta branch pruning bounding maximum lower thresholds ($\alpha$) and minimum upper thresholds ($\beta$), pruning dominated branches and reducing effective branch factors from $b^d$ toward $b^{d/2}$.
  * Expectimax search modeling non-optimal and stochastic adversary policies via expectation nodes.
  * Multi-attribute non-terminal board evaluation functions balancing food distance gradients, ghost hazard zones, and power capsule timers.
* **[`projects/ReinforcementLearning/Othello/`](projects/ReinforcementLearning/)**:
  * Dual-language (Python & Java) adversarial game-playing engine for Othello / Reversi.
  * Minimax tree search with Alpha-Beta pruning, bitboard mobility evaluation, and positional corner-weight heuristics.

---

### 3. Markov Decision Processes (MDPs) & Dynamic Programming
* **[`projects/pacmanAi3/`](projects/pacmanAi3/)**:
  * Formalized discrete state transitions $(S, A, T, R, \gamma)$ solved via offline dynamic programming.
  * Synchronous Batch Value Iteration computing exact Bellman optimality fixed points.
  * Asynchronous cyclic in-place value iteration accelerating intra-cycle convergence.
  * Prioritized Sweeping Value Iteration tracking Bellman error residuals via priority queues for targeted state updates.

---

### 4. Reinforcement Learning & Value Function Approximation
* **[`projects/pacmanAi3/`](projects/pacmanAi3/)**:
  * Model-free Temporal Difference (TD) Q-learning with $\epsilon$-greedy exploration schedules.
  * Approximate Q-learning with linear value function approximation ($Q(s, a) = \sum w_i f_i(s, a)$) trained online via gradient descent.
  * Applied across physical crawling robots (`crawler.py`), stochastic Gridworlds (`gridworld.py`), and multi-adversary game boards (`pacman.py`).
* **[`projects/ReinforcementLearning/RL/`](projects/ReinforcementLearning/)**:
  * **Stochastic Multi-Armed Bandits (`RL/bandit/`):** Adaptive exploration algorithms with exponential decay schedules solving non-stationary reward distributions, achieving $>35\%$ cumulative reward over reference baselines.
  * **Autonomous Pong Controller (`RL/pong/`):** Discretized spatial telemetry Q-learning agent optimizing continuous motor control for 2D arcade physics.

---

## Directory Structure

```text
reinforcement-learning-game-ai/
├── README.md
├── .gitignore
└── projects/
    ├── ReinforcementLearning/
    │   ├── README.md
    │   ├── Othello/
    │   │   ├── Java/
    │   │   ├── Python/
    │   │   └── test_code/
    │   └── RL/
    │       ├── README.md
    │       ├── bandit/
    │       └── pong/
    ├── pacmanAi/
    │   ├── README.md
    │   └── Search/
    ├── pacmanAi2/
    │   ├── README.md
    │   └── multiagents/
    └── pacmanAi3/
        ├── README.md
        ├── qlearningAgents.py
        ├── valueIterationAgents.py
        ├── crawler.py
        ├── gridworld.py
        └── pacman.py
```

---

## Technology Stack & Algorithms

* **Programming Languages:** Python 3, Java, Bash.
* **Mathematical & AI Domains:** Reinforcement Learning, Markov Decision Processes, Dynamic Programming, Game Theory, Graph Search, Multi-Armed Bandits.
* **Core Algorithms:** A\* Search, BFS, DFS, UCS, Minimax, Alpha-Beta Pruning, Expectimax, Value Iteration, Prioritized Sweeping, Q-Learning, Approximate Q-Learning, $\epsilon$-Greedy Bandit Optimization.
* **Simulation Environments:** Berkeley AI Simulation Engine, OpenAI Gym / `ma-gym` Pong, Custom 2-Joint Robot Physics Simulator.
