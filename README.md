# Frozen Lake with Q-Learning
in this repo I solve frozen lake using Q-Learning in combination with credit assignment, with is_slippery set to false. In all files the same strategy is used.
- Initialize a Q-Table with 0s for each observation and action combination
- assign a -2 for an action in an observation that leads to falling into a hole
- assign -1 to an action in an observation that keeps the agent in the same observation
- Actions are chosen randomly, but actions that have a reward of < 0 are filtered away
- If the gift is reached, assign credit to each previous step, whereas the reward given becomes smaller the longer ago the step was (this was bugged in 4x4 and 8x8)

Changes per notebook:
- **4x4 and 8x8**: Notebook has a bug in the credit assignment, resulting in the agent to sometimes get stuck in loops. Also, this notebook makes use of decreasing exploration which is nonoptimal. 
- **16x16 and 32x32**: Starting from 16x16, I fixed the credit assignment bug. The agent now doesnt overwrite rewards that are bigger. Elevate the max episode step from 500 to 1000. Also started making use of epochs starting from this notebook.
- **64x64**: Elevated max steps to 5000 and made use of more epochs. Also started using a consistent exploration rate of 1 to enhance efficiency. 
- **128x128**: Tried to solve 128x128 but couldn't make it work. Tried to add a new strategy whereas the agent would repeat the same action as many times as possible as long as the expected reward is >= 0. This allowed the agent to make more distance and prevent it from moving around in circles, but even this didn't manage to fix it.

Notebooks:
- [4x4 Notebook](./4x4.ipynb)
- [8x8 Notebook](./8x8.ipynb)
- [16x16 Notebook](./16x16.ipynb)
- [32x32 Notebook](./32x32.ipynb)
- [64x64 Notebook](./64x64.ipynb)

