# Quantum_Reinforcement_Learning

This repository contains a simple demonstration of **Quantum Policy Gradient Reinforcement Learning** using **PennyLane**. The project implements a quantum variational circuit as a policy network to solve a **1D grid navigation task**. The agent learns to move from a starting position to a goal position using **policy gradient updates**.

---

## Table of Contents
- [Overview](#overview)
- [Environment](#environment)
- [Quantum Policy Network](#quantum-policy-network)
- [Training](#training)
- [Evaluation](#evaluation)
- [Requirements](#requirements)
- [Usage](#usage)
- [References](#references)

---

## Overview
The notebook demonstrates how a **quantum circuit** can be used to model a stochastic policy for reinforcement learning. Specifically, it shows:

- How to define a **simple grid environment**.
- How to implement a **2-qubit variational quantum circuit** as a policy network.
- How to train the policy using **REINFORCE (policy gradient)**.
- How to visualize the agent’s path during evaluation.

This serves as a minimal example of **quantum reinforcement learning (QRL)** suitable for educational and research purposes.

---

## Environment
The environment is a simple **1D grid**:

- Grid size: 5 cells (positions 0 to 4)
- Start state: 0
- Goal state: 4
- Actions:
  - `0` → move left
  - `1` → move right
- Reward: `+1` when reaching the goal, otherwise `0`

The environment is implemented in the `SimpleGridEnv` class in the notebook.

---

## Quantum Policy Network
The quantum policy is implemented using **PennyLane**:

- **Number of qubits**: 2
- **Variational Circuit**: Each qubit applies RY and RZ rotations parameterized by learnable weights, followed by a CNOT gate for entanglement.
- **Policy Output**: The expectation values of the Pauli-Z operator on each qubit are converted into probabilities for action selection.
- **Action Selection**: Actions are sampled stochastically according to the policy probabilities.

---

## Training
Training uses a simple **policy gradient update**:

1. Sample an action from the quantum policy.
2. Take a step in the environment and receive a reward.
3. Compute the loss: `-log(prob(action)) * reward`
4. Compute the gradient of the loss w.r.t. the circuit parameters using PennyLane.
5. Update the parameters with gradient descent.

The notebook uses **50 training episodes** and a learning rate of **0.1**.

> Note: This implementation uses single-step rewards for simplicity. For longer tasks, you may implement **cumulative discounted rewards**.

---

## Evaluation
After training, the policy is evaluated over multiple episodes:

- The agent’s path is recorded for each episode.
- Paths are visualized using **Matplotlib**.

Each plot shows the agent’s progression from start to goal in the 1D grid.

---

## Requirements
To run this notebook, you need:

- Python 3.8+
- PennyLane
- NumPy
- Matplotlib

Install dependencies via pip:

```bash
pip install pennylane pennylane-numpy matplotlib
```

---

## Usage
1. Clone the repository:

```bash
git clone https://github.com/arunpandianj/Quantum_Reinforcement_Learning.git
cd Quantum_Reinforcement_Learning
```

2. Open the Jupyter Notebook:

```bash
jupyter notebook quantum_policy_rl.ipynb
```

3. Run the notebook cell by cell to:

- Train the quantum policy network
- Evaluate and visualize the agent’s path

---

## References
- [PennyLane Documentation](https://pennylane.ai/)
- Sutton, R. S., & Barto, A. G. (2018). *Reinforcement Learning: An Introduction*.
- Schuld, M., & Petruccione, F. (2018). *Supervised Learning with Quantum Computers*.

---

## License
This repository is released under the MIT License. Feel free to use and modify for educational and research purposes.

---

**Author**: Arun Pandian  
**GitHub**: [arunpandianj](https://github.com/arunpandianj)
