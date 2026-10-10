# Algorithm and Methodology Justification

This note describes the choices documented in the Group 42 notebook and refactored script. The experiment is a partial reproduction of the DQN approach on Breakout, not a replication of the original seven-game results.

## Why DQN?

Breakout has a discrete action space and visual observations. DQN approximates the action-value function \(Q(s,a)\) with a neural network instead of storing a separate value for every possible state. The convolutional layers learn visual features from the preprocessed game frames, and the output layer estimates values for the available actions.

## Input representation

The notebook uses the following pipeline:

1. Receive an RGB observation of shape 210 × 160 × 3.
2. Convert it to grayscale.
3. Resize to 84 × 110 and crop vertically to 84 × 84.
4. Stack the last four processed frames to obtain a state of shape 4 × 84 × 84.

Stacking frames supplies short-term temporal information that a single frame cannot provide on its own.

## DQN architecture

The network used in the notebook is:

- Convolution 1: 16 filters, kernel 8 × 8, stride 4, followed by ReLU.
- Convolution 2: 32 filters, kernel 4 × 4, stride 2, followed by ReLU.
- Flatten, then fully connected layer with 256 units and ReLU.
- Output layer with one Q-value per available action.

The action is selected with an epsilon-greedy policy: with probability epsilon the agent explores; otherwise it selects the action with the largest predicted Q-value.

## Why experience replay?

Neighboring game transitions are correlated. The implementation stores transitions \((s,a,r,s',done)\) in a 100,000-transition buffer and samples a random mini-batch of 32. Reusing randomly sampled experiences reduces the dependence on the most recent sequence and helps stabilize updates.

## Learning rule and parameters

The notebook's learning update uses the bootstrapped target:

\[
y = r + \gamma(1-done) \max_{a'} Q_{online}(s',a')
\]

The selected current-action Q-value is trained against this target using Smooth L1 loss. The optimizer is RMSProp with learning rate 0.00025; the discount factor is 0.99 and gradients are clipped to norm 10. Reward is clipped for learning to +1, 0, or −1.

**Implementation caveat:** the code computes the next-state value with the same online network; it does not implement a separate target network. The paper's original squared-error objective is also not identical to the Smooth L1 loss used in this notebook. These are implementation details to disclose when describing this as a partial reproduction.

## Training and evaluation protocol

- Environment: `ALE/Breakout-v5`
- Environment frameskip: 4; repeat-action probability: 0.0
- Training budget: 50,000 environment steps/frames as counted by the notebook loop
- Learning starts after 1,000 steps; network updates every 4 steps
- Epsilon schedule: 1.0 to 0.1 over 100,000 steps
- Evaluation: five episodes, epsilon = 0.05

## How the reported result was obtained

The executed notebook recorded 275 training episodes and a maximum observed episode reward of 5.0. The trained checkpoint was then loaded for five evaluation episodes. Each recorded reward was 0.0, so the mean evaluation reward was 0.0.

These are the measured results of this reduced-budget experiment. They do not show that the agent matched the original paper's performance. See the [notebook](../notebooks/Group42_DQN_Breakout_Reproduction.html), [result summary](../results/results_summary.csv), [evaluation CSV](../results/evaluation_results.csv), and [reward curve](../results/reward_curve.png).

## Primary reference

Mnih, V., et al. (2013). *Playing Atari with Deep Reinforcement Learning*. arXiv:1312.5602. https://arxiv.org/abs/1312.5602
