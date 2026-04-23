# Reproducing Q-Learning: A Comparative Study of Temporal Difference Algorithms

**CS 5100 – Foundations of Artificial Intelligence | Northeastern University**  
**Narmatha Kathiravan | Spring 2026**

---

## Overview

This project empirically reproduces the convergence of Q-learning as formally proved by Watkins and Dayan (1992) and extends the study into a comparative analysis of three Temporal Difference algorithms across four custom environments of increasing difficulty.

The central claim being verified is that Q-learning converges to the true optimal action-values Q* with probability 1, given sufficient exploration and an appropriate learning rate. The project further compares Q-learning against SARSA and Double Q-learning to demonstrate the practical consequences of on-policy versus off-policy learning and the overestimation bias problem.

---

## Paper References

| Paper | Contribution |
|---|---|
| Watkins & Dayan (1992). *Q-Learning*. Machine Learning, 8, 279–292 | Primary paper — convergence proof |
| Rummery & Niranjan (1994). *On-Line Q-Learning Using Connectionist Systems* | SARSA — on-policy TD learning |
| van Hasselt (2010). *Double Q-learning*. NeurIPS | Double Q-learning — overestimation bias correction |

---

## Algorithms

| Algorithm | Type | Key Property |
|---|---|---|
| Q-learning | Off-policy | Always updates using max Q(s') — assumes optimal future |
| SARSA | On-policy | Updates using actual next action taken — honest about exploration |
| Double Q-learning | Off-policy | Two Q-tables decouple selection and evaluation — removes overestimation bias |

---

## Environments

All four environments were implemented from scratch as custom Python classes — no external RL libraries used.

| Environment | Size | Key Challenge |
|---|---|---|
| GridWorld (Deterministic) | 5×5, 25 states | Baseline convergence test |
| GridWorld (Stochastic) | 5×5, 25 states | 80/10/10 slip probability |
| CliffWalking | 4×12, 48 states | On-policy vs off-policy path behaviour |
| FrozenLake | 4×4, 16 states | Equal 1/3 slip + permanent failure states |

---

## Experiments

| Experiment | Environments | What it Tests |
|---|---|---|
| 1 — Convergence Comparison | GridWorld (det + sto) | Verifies Q-learning convergence theorem empirically |
| 2 — Effect of Learning Rate | GridWorld (det) | Demonstrates paper's learning rate convergence condition |
| 3 — Path Comparison | CliffWalking | On-policy vs off-policy behavioural difference |
| 4 — Overestimation Bias | GridWorld (det + sto) | Q-learning vs Double Q-learning value accuracy |
| 5 — Performance Under Uncertainty | FrozenLake | All three algorithms under maximum stochasticity |

---

## Key Results

- **Q-learning** converged to near-zero error in both GridWorld environments, directly confirming Watkins and Dayan's convergence theorem
- **SARSA** learned a safer 17-step path on CliffWalking versus Q-learning's aggressive 13-step cliff-edge path — direct evidence of on-policy caution
- **Double Q-learning** produced more stable and consistent value estimates than Q-learning in stochastic environments, consistent with van Hasselt (2010)
- **FrozenLake** proved genuinely difficult for all three algorithms — none achieved stable 50% success within 100,000 episodes, revealing the limits of tabular TD methods under maximum uncertainty
- **Reproducibility verdict:** Partially reproducible — empirical claims confirmed, exact theoretical conditions cannot be satisfied in finite training

---

## How to Run

### Requirements
- Python 3.8 or higher
- numpy
- matplotlib
- jupyter

### Installation
```bash
# Clone the repository
git clone https://github.com/narmathakathiravan98/q-learning.git
cd q-learning

# Install dependencies
pip install numpy matplotlib jupyter
```

### Running the Notebook
```bash
jupyter notebook Q-Learning-Capstone.ipynb
```

Run all cells from top to bottom. The notebook is self-contained — all environments, algorithms, Q* computation, and experiments are defined and run within the single notebook file.

**Expected runtime:** approximately 10–15 minutes for all training runs on a standard laptop.

---

## Experimental Parameters

| Parameter | Value |
|---|---|
| Learning rate (α) | 0.1 |
| Discount factor (γ) | 0.99 |
| Exploration rate (ε) | 0.3 (fixed for Q-learning and Double Q-learning, decaying for SARSA) |
| GridWorld episodes | 60,000 |
| CliffWalking episodes | 100,000 |
| FrozenLake episodes | 100,000 |
| Error recorded every | 100 episodes |

---

## Demo

Watch the project demo here:  
[https://northeastern.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=130ebbcc-0ec9-4c32-8b0b-b435014e723b](https://northeastern.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=130ebbcc-0ec9-4c32-8b0b-b435014e723b)

---

## Reproducibility Note

This project uses a fixed random seed (`np.random.seed(42)`) to ensure all results are reproducible. Running the notebook from top to bottom will produce the same plots and numerical results as reported in the final report.
