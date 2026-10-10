# Group 42 — DQN Breakout Partial Reproduction

This project is a **partial reproduction of the Deep Q-Network (DQN) methodology** described in:

> Volodymyr Mnih et al. (2013), *Playing Atari with Deep Reinforcement Learning*. arXiv:1312.5602.

Our implementation focuses on **Atari Breakout only** and uses a reduced training budget. It should not be interpreted as a reproduction of the original paper's reported performance across seven Atari games.

## Project scope

- **Environment:** `ALE/Breakout-v5`
- **Frameworks:** Gymnasium and PyTorch
- **Observation:** raw 210 × 160 × 3 RGB; preprocessed to 84 × 84 grayscale
- **State:** four stacked 84 × 84 frames
- **DQN architecture:** Conv(16 filters, 8×8, stride 4), Conv(32 filters, 4×4, stride 2), fully connected layer with 256 units, and an output per available action
- **Actions:** 4
- **Replay buffer capacity:** 100,000 transitions
- **Mini-batch size:** 32
- **Optimizer:** RMSProp
- **Learning rate:** 0.00025
- **Discount factor:** 0.99
- **Training budget:** 50,000 frames
- **Learning starts:** 1,000 frames
- **Training frequency:** every 4 frames
- **Evaluation exploration parameter:** epsilon = 0.05

## Results recorded in the executed notebook

The executed Colab notebook reports:

| Metric | Recorded result |
|---|---:|
| Training frames | 50,000 |
| Training episodes | 275 |
| Maximum observed training episode reward | 5.0 |
| Evaluation episodes | 5 |
| Mean evaluation reward | 0.0 |

Each of the five evaluation episodes recorded reward 0.0. This result indicates that the reduced-budget experiment did **not** achieve effective Breakout performance during evaluation. We present it transparently and do not claim to have matched the original paper's results.

## Method overview

1. Initialize the Breakout environment.
2. Convert observations to grayscale, resize to 84 × 84, and stack four frames.
3. Estimate action values with a convolutional DQN.
4. Store state/action/reward/next-state transitions in a replay buffer.
5. Sample mini-batches and update the network using a Q-learning target.
6. Save a model checkpoint, then evaluate with epsilon = 0.05.
7. Report the measured training and evaluation outcomes.

## Team contributions

| Member | Stated contribution |
|---|---|
| Ashutosh Gupta | Paper analysis and methodology |
| Vipul Gupta | DQN architecture and replay implementation |
| Aniket Bhutani | Colab training/evaluation pipeline |
| Rajat Pali | Results analysis and visualization |

See [docs/contributions.md](docs/contributions.md) for the evidence plan and contribution mapping. This table documents the team's declared division of work; it is not a substitute for individual Git commits or other independent evidence.

## Resources

- **Research paper:** [Mnih et al. (2013), arXiv:1312.5602](https://arxiv.org/abs/1312.5602)
- **Gymnasium documentation:** [Gymnasium](https://gymnasium.farama.org/)
- **PyTorch documentation:** [PyTorch](https://pytorch.org/docs/stable/index.html)
- **Environment API:** [ALE Breakout v5](https://ale.farama.org/environments/breakout/)

## Reproducibility

The original work was executed in Google Colab. To reproduce the experiment, use the executed notebook and source code added to this repository once available. The configuration above documents the reduced-budget run; results can vary with software versions, environment setup, random seeds, and hardware.

> **Evidence status:** The original executed HTML notebook was supplied during preparation of this repository, but the notebook file and separate generated CSV/graph/checkpoint artifacts have not yet been uploaded here. Add the actual files before treating the repository as the complete code-and-results package.

## Limitations

- This is a partial reproduction on one game, not the original seven-game experiment.
- The training budget is 50,000 frames, much smaller than the original experiment.
- Five evaluation episodes are a small evaluation sample.
- The measured mean evaluation reward was 0.0; successful game-playing performance was not demonstrated.

## Citation

If you use this repository, please cite the original paper:

Mnih, V., et al. (2013). *Playing Atari with Deep Reinforcement Learning*. arXiv:1312.5602. https://arxiv.org/abs/1312.5602
