# Monte Carlo Game Agent

A Python implementation of a **Monte Carlo Tree Search (MCTS)** agent for the MiniStS environment — a simplified, headless version of *Slay the Spire*.  
This project focuses on strategic decision-making under uncertainty using simulation-based planning.

---

## Overview
I implemented a complete MCTS agent that selects actions by exploring simulated game states and learning from rollouts.  
Each decision balances exploration of new strategies and exploitation of known good ones through the **UCB-1** selection rule.

The project uses the MiniStS engine as a testbed, allowing me to test the MCTS agent against other bots such as the Sampling Bot and Backtrack Bot.

---

## How It Works

### MCTS Cycle
Each decision step runs through four phases:

1. **Selection:**  
   Traverse the tree using UCB-1 until reaching a node with unexplored actions.
2. **Expansion:**  
   Add one new child node for an untried action.
3. **Rollout (Simulation):**  
   Play out random moves until the game ends and return the resulting reward.
4. **Backpropagation:**  
   Propagate the outcome back through the visited nodes to update average values.

The agent repeats this process for a fixed number of iterations before choosing the best action.

---

## Technical Details
- **Selection Strategy:** UCB-1 formula  

- **Constant (c):** 0.5 — tuned for balanced exploration/exploitation  
- **Iterations per turn:** 50  

All implementation details — tree structure, node expansion, and rollout control — are handled in `agent.py` using a custom `TreeNode` class.

---

## Performance

Each configuration was tested for 20 games per scenario.  
Results compared to the baseline Sampling Bot:

| Scenario | Sampling Bot | MCTS Agent |
|-----------|---------------|------------|
| Giant | 100% | 100% |
| Offerings | 80% | 85% |
| Low HP | 60% | 70% |

The MCTS agent consistently outperformed or matched the baseline across all test cases.

---

## Challenges
- Getting consistent results in the low HP scenario required refining expansion behavior and balancing how often weak nodes were revisited.  
- Tuning `c` was crucial — too high caused random behavior, too low caused the agent to get stuck.  
- Debugging unreturned plans and broken rollouts revealed how easily small logical issues can destabilize the search.

This project gave me hands-on insight into how **probabilistic search** works in practice and how fine-tuning affects strategic consistency.

---

## Files
| File | Description |
|------|--------------|
| `main.py` | Entry point to run the MCTS agent |
| `agent.py` | Core implementation of the Monte Carlo Tree Search |
| `battle.py` | Turn management and battle simulation |
| `card.py` | Defines cards, effects, and player actions |
| `game.py` | Core game logic |
| `config.py` | Parameters like iteration count and constant `c` |
| `status_effects.py` | Defines buffs and debuffs in battles |
| `asgn6 146 report.pdf` | Implementation summary and testing results |
| `LICENSE` | License information |

---

## Run the Agent

### Install Dependencies
```bash
pip install -r requirements.txts