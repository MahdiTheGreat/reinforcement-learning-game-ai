# Multi-Agent Adversarial Search & Game Theory

An adversarial game-playing framework implementing multi-agent decision models, game-tree search algorithms, and heuristic state evaluators in competitive multi-adversary environments.

---

## Adversarial Decision Architectures

```
                           MAX (Pacman)
                                │
               ┌────────────────┴────────────────┐
               ▼                                 ▼
         MIN 1 (Ghost 1)                   MIN 1 (Ghost 1)
               │                                 │
         ┌─────┴─────┐                     ┌─────┴─────┐
         ▼           ▼                     ▼           ▼
       MIN 2       MIN 2                 MIN 2       MIN 2
```

### 1. Multi-Agent Minimax (`MinimaxAgent`)
* **Game-Tree Structure:** Extends classical 2-player zero-sum minimax to $1 + k$ agents (one maximizing player and $k$ minimizing adversaries per complete ply).
* **Recursive Formulation:**
  * For MAX player ($p = 0$):

$$V(s) = \max_{a \in \text{Actions}(s)} V(\text{Result}(s, a))$$

  * For MIN players ($p \in \{1, \dots, k\}$):

$$V(s) = \min_{a \in \text{Actions}(s)} V(\text{Result}(s, a))$$

* Recursion increments the effective search depth only after all $k$ minimizing agents have completed their turn.

### 2. Alpha-Beta Branch Pruning (`AlphaBetaAgent`)
* **Optimization Mechanism:** Preserves minimax decision optimality while pruning branches that are provably dominated:
  * $\alpha$: The maximum lower-bound value discovered by MAX along the path to the root.
  * $\beta$: The minimum upper-bound value discovered by MIN along the path to the root.
* **Pruning Criteria:** Whenever $v < \alpha$ during a MIN node update or $v > \beta$ during a MAX node update, remaining sibling branches are truncated immediately ($\beta \le \alpha$).
* **Performance Gain:** In structured game trees, reduces effective branch factor from $b^d$ toward $b^{d/2}$, allowing search horizons to reach twice the depth of standard minimax within equivalent compute budgets.

### 3. Expectimax Probabilistic Search (`ExpectimaxAgent`)
* **Stochastic Modeling:** Replaces worst-case adversarial assumptions with probabilistic expected value nodes for environments where adversaries act sub-optimally or follow stochastic behavior distributions:

$$V(s) = \sum_{a \in \text{Actions}(s)} P(a \mid s) \cdot V(\text{Result}(s, a))$$

* Allows the agent to take calculated risks and exploit suboptimal enemy policies (such as random walk or noisy patrol routines) rather than overly conservative avoidance.

---

## State Evaluation Function Design (`betterEvaluationFunction`)

For search trees exceeding the terminal depth limit, intermediate non-terminal board states are ranked using a multi-factor linear evaluation function:

$$\text{Score}(s) = \text{GameScore}(s) + w_1 \cdot \frac{1}{d_{\text{closest\_food}}} + w_2 \cdot d_{\text{active\_ghost}} + w_3 \cdot \frac{1}{d_{\text{scared\_ghost}}} - w_4 \cdot N_{\text{food}} - w_5 \cdot N_{\text{capsules}}$$

### Feature Weights & Behavioral Dynamics
1. **Closest Pellet Reciprocal Distance ($w_1$):** Provides continuous gradient guidance toward adjacent food, eliminating stagnation in open maze corridors.
2. **Active Ghost Proximity ($w_2$):** Imposes severe non-linear penalties when active ghosts approach within 2 grid units, triggering evasive path deviations.
3. **Scared Ghost Hunting Bonus ($w_3$):** Inverts avoidance behavior into aggressive interception whenever power capsule timers are active, capturing high-reward ghost bounties.
4. **Food & Capsule Penalties ($w_4, w_5$):** Penalizes residual inventory count, prioritizing board clearing over wandering.
