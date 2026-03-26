# Frozen Lake with Q-table ❄️
This project solves the **Frozen Lake** environment from [Gymnasium](https://gymnasium.farama.org/) using a **custom RL-inspired approach** combined with **credit assignment**. Six grid sizes are tackled — from a trivial 4×4 up to a challenging 128×128 — with each notebook building on lessons learned from the previous one.

> **Important**: All notebooks use `is_slippery=False` and assume no prior knowledge of the gift's location (it is always in the bottom right when using the provided map generator).

## Table of Contents
- [Strategy](#strategy)
- [Changes Per Notebook](#changes-per-notebook)
- [Results](#results)
- [Possible Future Improvements](#possible-future-improvements)

## Strategy
The general approach used across all notebooks:

1. Initialize the Q-Table with `0` for every observation-action pair.
2. Assign `-2` to any action that causes the agent to fall into a hole.
3. Assign `-1` to any action that leaves the agent in the same cell (stuck against a wall).
4. Filter out actions with reward `< 0` during random exploration.
5. On reaching the gift, back-propagate decayed credit to every step in the episode history.
6. Stop training as soon as a valid path to the gift is found **(No path optimization is performed)**.

## Changes Per Notebook

| Notebook | Key Changes |
|---|---|
| **4×4** | Baseline implementation. Credit assignment has a bug, larger rewards can be overwritten, causing the agent to loop. Epsilon decays over time. |
| **8×8** | Same code as 4×4, bug still present. |
| **16×16** | Credit assignment bug fixed, rewards are only overwritten if the new value is larger. Max episode steps raised from 500 → 1000. Epochs introduced. |
| **32×32** | Max steps raised to 1000. More epochs added to handle the larger search space. |
| **64×64** | Max steps raised to 5000. Exploration rate fixed at `1` (no decay) for the full run, making sure every frame is spent trying to explore to maximize efficiency. |
| **128×128** | Strategy revised and code fully revised for maximum efficiency. Read notebook for full explanation |

## Results
Every notebook successfully reaches the gift. Training stops as soon as the first valid path is discovered, the path is not guaranteed to be optimal. Theoretically, you could continue expanding the map forever. Finding the gift is just a game of chance, hoping your agent moves down and right enough times to reach the gift.

*Image of the generated 128×128 map, the largest map I played:*

<img width="638" height="676" alt="128x128 map" src="https://github.com/user-attachments/assets/cc98b9d1-b174-4025-9a39-9888015502cd" />

## Possible Future Improvements
- Continue training after finding the gift using random exploration to discover shorter paths.
- Bias the action selection toward moving down and right, since the gift is always in the bottom-right corner.
