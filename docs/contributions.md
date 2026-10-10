# Individual Contributions and Proof-of-Work Map

The following division of work was supplied by Group 42. The linked repository files provide traceable project artifacts to demonstrate during the recording.

| Member | Declared contribution | What to show in the demonstration | Repository evidence |
|---|---|---|---|
| Ashutosh Gupta | Paper analysis and methodology | PPT motivation, paper contribution, Q-learning flow, experiment scope, and limitations | [README and scope](../README.md), [references](REFERENCES.md), [original paper](https://arxiv.org/abs/1312.5602) |
| Vipul Gupta | DQN architecture and replay implementation | HTML notebook DQN model and replay-buffer cells; explain the 16/32/256 architecture and replay sampling | [Executed notebook](../notebooks/Group42_DQN_Breakout_Reproduction.html), [refactored implementation](../src/breakout_dqn.py) |
| Aniket Bhutani | Colab training/evaluation pipeline | HTML notebook's final training lines, checkpoint path, and five evaluation episode outputs | [Executed notebook](../notebooks/Group42_DQN_Breakout_Reproduction.html), [evaluation CSV](../results/evaluation_results.csv), [training episode output summary](../results/training_episode_summary_from_notebook_output.csv) |
| Rajat Pali | Results analysis and visualization | Reward curve, final metrics, evaluation result, and interpretation of limitations | [Reward curve](../results/reward_curve.png), [results summary](../results/results_summary.csv), [results notes](../results/README.md) |

## Measured evidence from the executed notebook

- Training budget: 50,000 frames
- Recorded training episodes: 275
- Maximum observed training episode reward: 5.0
- Evaluation episodes: 5
- Each evaluation episode reward: 0.0
- Mean evaluation reward: 0.0

The CSV named `training_episode_summary_from_notebook_output.csv` was derived from the 275 console lines embedded in the executed notebook. It contains episode, frame, reward, and epsilon. It deliberately does not claim to be the original training CSV because the console output does not include every loss value.

## What this repository does and does not prove

- The executed notebook, code, results files, and images make the method and recorded run inspectable.
- The contribution table records the team's stated roles; repository contents alone do not prove which person authored each piece of work.
- For stronger individual evidence, each member should make a **genuine commit or pull request under their own GitHub account** for their actual contribution, or provide another verifiable work artifact. Do not fabricate commit authorship or backdate work.
- The current script is a refactored version of the notebook pipeline, while the executed HTML notebook remains the primary record of the recorded experiment.

## Project scope

This is a **partial reproduction of the DQN methodology on Breakout only**, using a reduced 50,000-frame training budget. It does not reproduce the original paper's full seven-game experiment or its reported performance.
