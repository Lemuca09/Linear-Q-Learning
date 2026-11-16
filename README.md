<div align="center">

# 🧠 Linear Q-Learning in Haskell

**Reinforcement learning without the Q-table.**
A pure functional agent that learns compact, generalizable policies through linear value-function approximation.

<br>

![Haskell](https://img.shields.io/badge/Haskell-5D4F85?style=for-the-badge&logo=haskell&logoColor=white)
![Cabal](https://img.shields.io/badge/Build-Cabal-0A7BBB?style=for-the-badge)
![Reinforcement Learning](https://img.shields.io/badge/AI-Reinforcement%20Learning-E8590C?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-2EA44F?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Functional-brightgreen?style=for-the-badge)

</div>

---

## ✨ Overview

Classic tabular Q-Learning stores one value per state-action pair. That works for toy problems and collapses as the state space grows.

**Linear Q-Learning** replaces the table with a weight vector. Each Q-value is computed as a dot product between learned weights and a feature representation of the state-action pair:

```
Q(s, a) = wᵀ · φ(s, a)
```

The result is an agent whose memory footprint is fixed by the number of features, and whose knowledge transfers between similar states.

---

## 🚀 Highlights

<table>
  <tr>
    <td align="center" width="33%">
      <h3>📐 Linear Approximation</h3>
      <p>Q-values as <code>wᵀ·φ(s, a)</code> with a configurable feature mapping.</p>
    </td>
    <td align="center" width="33%">
      <h3>📉 TD Learning</h3>
      <p>Online weight updates driven by the temporal-difference error.</p>
    </td>
    <td align="center" width="33%">
      <h3>🎲 ε-Greedy Policy</h3>
      <p>Exploration with a tunable decay schedule.</p>
    </td>
  </tr>
  <tr>
    <td align="center" width="33%">
      <h3>λ Pure Functional</h3>
      <p>Immutable state and explicit transitions for reproducible runs.</p>
    </td>
    <td align="center" width="33%">
      <h3>📊 Learning Diagnostics</h3>
      <p>Episode rewards, weight evolution and policy behavior over training.</p>
    </td>
    <td align="center" width="33%">
      <h3>⚖️ Tabular Baseline</h3>
      <p>Built-in tabular agent for side-by-side comparison.</p>
    </td>
  </tr>
</table>

---

## ⚙️ How It Works

<table>
  <tr>
    <td align="center" width="20%"><h3>1️⃣</h3><b>Observe</b><br><sub>Read the current state and build φ(s, a) for each action</sub></td>
    <td align="center" width="20%"><h3>2️⃣</h3><b>Estimate</b><br><sub>Compute Q-values as wᵀ·φ(s, a)</sub></td>
    <td align="center" width="20%"><h3>3️⃣</h3><b>Act</b><br><sub>Pick an action with ε-greedy and collect the reward</sub></td>
    <td align="center" width="20%"><h3>4️⃣</h3><b>Update</b><br><sub>Adjust the weights using the TD error</sub></td>
    <td align="center" width="20%"><h3>5️⃣</h3><b>Repeat</b><br><sub>Iterate until the policy converges</sub></td>
  </tr>
</table>

**Weight update rule**

```
δ = r + γ · maxₐ' Q(s', a') − Q(s, a)
w ← w + α · δ · φ(s, a)
```

| Symbol | Meaning |
|:---:|---|
| `α` | Learning rate |
| `γ` | Discount factor |
| `ε` | Exploration rate |
| `φ(s, a)` | Feature vector for a state-action pair |
| `w` | Learned weight vector |
| `δ` | Temporal-difference error |

---

## 🆚 Tabular vs. Linear Approximation

<table>
  <tr>
    <th></th>
    <th align="center">Tabular Q-Learning</th>
    <th align="center">Linear Approximation</th>
  </tr>
  <tr>
    <td><b>💾 Memory</b></td>
    <td>Grows with |S| × |A|</td>
    <td>Fixed by feature count</td>
  </tr>
  <tr>
    <td><b>🔗 Generalization</b></td>
    <td>None, each state is learned independently</td>
    <td>Similar states share knowledge</td>
  </tr>
  <tr>
    <td><b>🌌 Large / continuous spaces</b></td>
    <td>Impractical</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td><b>🎯 Convergence guarantees</b></td>
    <td>Strong</td>
    <td>Depends on feature design</td>
  </tr>
  <tr>
    <td><b>🛠️ Feature engineering</b></td>
    <td>Not required</td>
    <td>Required, and decisive for quality</td>
  </tr>
</table>

> **Trade-off:** linear approximation buys scalability and generalization at the cost of exact convergence guarantees. Choosing good features is what makes or breaks the agent.

---

## 📦 Installation

**Requirements**

- [GHC](https://www.haskell.org/ghc/) ≥ 9.2
- [Cabal](https://www.haskell.org/cabal/) ≥ 3.6 (or [Stack](https://docs.haskellstack.org/))

```bash
git clone https://github.com/Lemuca09/Linear-Q-Learning.git
cd Linear-Q-Learning
cabal build
```

## ▶️ Usage

```bash
# Train the linear agent and watch the learning process
cabal run linear-qlearning

# Compare against the tabular baseline
cabal run linear-qlearning -- --baseline tabular
```

> Adjust the executable name and flags to match your `.cabal` file.

---

## 📈 Results

The demo shows how the agent evolves during training:

<table>
  <tr>
    <td align="center" width="33%">
      <h3>📈 Reward Curve</h3>
      <p>Cumulative reward per episode as the policy improves.</p>
    </td>
    <td align="center" width="33%">
      <h3>🧮 Weight Evolution</h3>
      <p>How each feature weight stabilizes over time.</p>
    </td>
    <td align="center" width="33%">
      <h3>🏁 Final Policy</h3>
      <p>Learned behavior compared with the tabular baseline.</p>
    </td>
  </tr>
</table>

<!-- Replace with real charts or a GIF of the agent:
![Reward curve](docs/reward-curve.png)
![Agent demo](docs/demo.gif)
-->

---

## 🗂️ Project Structure

```
.
├── app/            # Entry point and demo runner
├── src/
│   ├── Environment.hs   # States, actions, rewards, transitions
│   ├── Features.hs      # Feature mapping φ(s, a)
│   ├── Agent.hs         # Linear Q-Learning agent and weight updates
│   ├── Tabular.hs       # Tabular baseline
│   └── Metrics.hs       # Diagnostics and reporting
├── docs/           # Charts and demo assets
└── *.cabal
```

> Adjust the tree to match the real layout of your repository.

---

## 🧭 Roadmap

- [ ] Eligibility traces (Q(λ))
- [ ] Alternative feature maps (polynomial, tile coding, RBF)
- [ ] Experience replay
- [ ] Additional environments

---

## 🤝 Contributing

Issues and pull requests are welcome. For larger changes, please open an issue first to discuss what you would like to change.

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

<div align="center">

<sub>Built with λ and curiosity.</sub>

</div>
