# Frozen Lake with Q-Learning
in this repository I solve frozen lake using Q-Learning in combination with credit assignment. Important to mention is that all notebooks make use of `is_slippery` set to false, and in all notebooks I assume I don't know where the gift is located (It is always bottom right). In all files generally the same strategy is used (if not it is mentioned in changes per notebook):
- Initialize a Q-Table with 0s for each observation and action combination
- assign a -2 for an action in an observation that leads to falling into a hole
- assign -1 to an action in an observation that keeps the agent in the same observation
- Actions are chosen randomly, but actions that have a reward of < 0 are filtered away
- If the gift is reached, assign credit to each previous step, whereas the reward given becomes smaller the longer ago the step was (this was bugged in 4x4 and 8x8)
- The path is not optimized, once a path to the gift is found, training is stopped.

## Changes per notebook:
- **4x4 and 8x8**: Notebook has a bug in the credit assignment, resulting in the agent to sometimes get stuck in loops. Also, this notebook makes use of decreasing exploration which is nonoptimal. 
- **16x16 and 32x32**: Starting from 16x16, I fixed the credit assignment bug. The agent now doesnt overwrite rewards that are bigger. Elevate the max episode step from 500 to 1000. Also started making use of epochs starting from this notebook.
- **64x64**: Elevated max steps to 5000 and made use of more epochs. Also started using a consistent exploration rate of 1 to enhance efficiency. 
- **128x128**: In the 128x128 notebook the code has completely been revised, ensuring maximum efficiency, still trying to reach the gift without making assumptions.
- Note: Theoretically, you could continue this proces forever. Finding the gift is just a game of chance, hoping your agent moves down and right enough times to get to the gift. To make this project more efficient, you could keep training after reaching the gift in combination with random moves to try to shorten the path to the gift. Also could you tell the agent that moving down and right are preferred over moving up and left.

## Notebooks:
- [4x4 Notebook](./4x4.ipynb)
- [8x8 Notebook](./8x8.ipynb)
- [16x16 Notebook](./16x16.ipynb)
- [32x32 Notebook](./32x32.ipynb)
- [64x64 Notebook](./64x64.ipynb)
- [128x128 Notebook](./128x128.ipynb)

