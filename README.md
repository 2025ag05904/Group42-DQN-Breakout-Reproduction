# Group 42 — DQN Breakout Partial Reproduction

This project is a **partial reproduction of the Deep Q-Network (DQN) methodology** described in:

> Volodymyr Mnih et al. (2013), *Playing Atari with Deep Reinforcement Learning*. arXiv:1312.5602.

Our implementation focuses on **Atari Breakout only** and uses a reduced training budget. It is not a reproduction of the original paper's seven-game experiment or reported performance.

## Project artifacts

- [Executed HTML notebook](notebooks/Group42_DQN_Breakout_Reproduction.html) — notebook code and captured outputs from the Colab run.
- [Refactored runnable training/evaluation script](src/breakout_dqn.py) — implementation based on the notebook's model, replay, training, and evaluation logic.
- [Training episode summaries](results/training_episode_summary_from_notebook_output.csv) — 275 episode records transcribed from the executed notebook's console output. This file excludes the original CSV's loss column because loss values were not printed for every episode.
- [Evaluation results](results/evaluation_results.csv) — five measured evaluation rewards and summary values.
- [Results summary](results/results_summary.csv) — key metrics recorded by the notebook.
- [Reward curve](results/reward_curve.png) — graph embedded in the executed notebook.
- [Environment frame](screenshots/raw_breakout_frame.png) and [preprocessed frame](screenshots/preprocessed_frame.png) — notebook-generated illustrations of the input pipeline.
- [Contribution/evidence mapping](docs/contributions.md).
- [References](docs/REFERENCES.md).

## Scope and method

- **Environment:** `ALE/Breakout-v5`
- **Frameworks:** Gymnasium and PyTorch
- **Raw observation:** 210 × 160 × 3 RGB
- **Preprocessing:** 84 × 84 grayscale
- **State:** four stacked 84 × 84 frames
- **DQN:** Conv(16 filters, 8×8, stride 4), Conv(32 filters, 4×4, stride 2), fully connected layer with 256 units, output per action
- **Actions:** 4
- **Replay buffer:** 100,000 transitions
- **Mini-batch:** 32
- **Optimizer:** RMSProp
- **Learning rate:** 0.00025
- **Discount factor:** 0.99
- **Training budget:** 50,000 frames
- **Learning starts:** 1,000 frames
- **Training frequency:** every 4 frames
- **Evaluation epsilon:** 0.05

## Results from the executed notebook

| Metric | Recorded value |
|---|---:|
| Training frames | 50,000 |
| Training episodes | 275 |
| Maximum observed training episode reward | 5.0 |
| Evaluation episodes | 5 |
| Mean evaluation reward | 0.0 |

All five evaluation episodes recorded reward 0.0. The reduced-budget run therefore **did not demonstrate effective Breakout performance**. We report this honestly and do not claim to match the original paper's performance.

## Run the refactored script

Use Python with the Atari dependencies and an available Breakout ROM. Installation commands can differ by platform and CUDA version; select the suitable PyTorch build using the [official PyTorch installation guide](https://pytorch.org/get-started/locally/).

```bash
pip install -r requirements.txt
python src/breakout_dqn.py --output-dir results
```

The script saves a training log, model checkpoint, evaluation CSV, summary CSV, and reward curve under the selected output directory. A fresh run may produce different scores depending on the environment, dependencies, and hardware. The published CSVs and reward curve in this repository are evidence extracted from the submitted executed notebook, not results from a newly rerun script.

## Team contributions

| Member | Stated contribution |
|---|---|
| Ashutosh Gupta | Paper analysis and methodology |
| Vipul Gupta | DQN architecture and replay implementation |
| Aniket Bhutani | Colab training/evaluation pipeline |
| Rajat Pali | Results analysis and visualization |

See [docs/contributions.md](docs/contributions.md). The table records the stated division of work; it does not, by itself, independently prove authorship. Genuine individual commits and screenshots of each person's work should be added if available.

## Limitations

- Partial reproduction on one game only, not all seven games from the paper.
- A 50,000-frame budget, much smaller than the original experiment.
- Only five evaluation episodes.
- Mean evaluation reward 0.0; strong task performance was not achieved.
- The script is a refactored version of the notebook logic; the executed HTML notebook remains the primary record of the recorded run.

## Citation

Mnih, V., et al. (2013). *Playing Atari with Deep Reinforcement Learning*. arXiv:1312.5602. https://arxiv.org/abs/1312.5602
