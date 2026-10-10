# Video Demonstration Guide (6 minutes)

Use the PPT for the research explanation and this repository's executed HTML for implementation evidence. Have each requested notebook section open before recording; avoid scrolling through unrelated cells.

| Time | Speaker | Show | Evidence point |
|---|---|---|---|
| 0:00–1:25 | Ashutosh | PPT slides 1–4 | Motivation, paper contribution, and DQN learning loop |
| 1:25–2:10 | Vipul | PPT slides 5–6 | Architecture and experience replay rationale |
| 2:10–2:55 | Vipul | HTML notebook, model and replay cells | Actual DQN / replay implementation; point out 16/32/256, replay capacity 100,000, RMSProp |
| 2:55–3:30 | Aniket | PPT implementation slide | Environment, preprocessing, frame stack, and reduced 50,000-frame budget |
| 3:30–4:25 | Aniket | HTML training output and evaluation output | Training completion, 275 episodes, saved checkpoint, five evaluation scores |
| 4:25–5:00 | Rajat | PPT results slide | Scope distinction: original paper versus our partial reproduction |
| 5:00–5:30 | Rajat | HTML final results and repository CSVs | Measured results: maximum training reward 5.0 and mean evaluation reward 0.0 |
| 5:30–6:00 | Rajat | PPT limitations, reference and conclusion slides | Limitations, honest interpretation, and citation |

## Individual proof-of-work mapping

- Ashutosh Gupta — paper analysis and methodology: PPT motivation/methodology/limitations slides and [references](REFERENCES.md).
- Vipul Gupta — DQN architecture and replay implementation: [notebook](../notebooks/Group42_DQN_Breakout_Reproduction.html) model/replay sections and [refactored source](../src/breakout_dqn.py).
- Aniket Bhutani — Colab training/evaluation pipeline: notebook training output, checkpoint save, and [evaluation CSV](../results/evaluation_results.csv).
- Rajat Pali — results analysis and visualization: [reward curve](../results/reward_curve.png), [summary table](../results/results_summary.csv), and [training episode output](../results/training_episode_summary_from_notebook_output.csv).

The work split above records the team's stated roles and maps them to visible artifacts. For independently verifiable authorship, each contributor should add their own genuine commit or pull request; do not fabricate commit authorship.
