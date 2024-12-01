# Q-Learning Based Autonomous Navigation in Grid Environments

---

## Introduction

This project presents a Q-Learning based approach for autonomous navigation in grid environments. The performance of the Q-Learning agents is evaluated over multiple episodes, demonstrating their ability to learn optimal policies for navigation under both incomplete and complete information scenarios.

---

## Methodology

### Q-Learning Algorithm

The key components of the Q-Learning implementation include:

- **Learning Rate (\(\alpha\))**: 0.1
- **Discount Factor (\(\gamma\))**: 0.99
- **Exploration Rate (\(\epsilon\))**: 0.1

The grid environment, agents, and environments are coded by the author. A Q-table dictionary is used to save the temporal difference Q-values.

---

## Environment Setup

The environment consists of a grid where three agents navigate toward a target position while avoiding collisions with each other. The environment setup and problem formulation are inspired by decentralized UAV network models, where maintaining connectivity and avoiding collisions are critical [[1]](#references).

### Single Goal Environment

- The state space is defined by the positions of all agents.
- The goal's position is fixed at a specific grid location.

### Series of Goals Environment

- Each agent must reach a sequence of three goal positions, which are revealed one at a time.
- After reaching one goal, the next goal is assigned.
- The last target's reward value is set to 100,000 to encourage the models to reach the final target.

---

## Training and Evaluation

The Q-Learning agents were trained for 1,500,000 episodes, with each episode lasting up to 100 steps of movements.

- **Rewards and Penalties**:
  - Taking a step: -1 penalty
  - Reaching the goal: +10,000 reward
  - Collision: -10,000 penalty

A test episode size of 5,000 was used to obtain a mean reward value for each model. The agents' trajectories were visualized over 5 runs to evaluate their learning progress and policy optimization.

### Models Tested

Three Q-Learning models were tested with different action and state spaces. All models' state spaces include the positions of all agents.

1. **Shared Action Model**
   - Action space: Moving up, down, left, or right for all agents simultaneously.
   - State-Action space: All possible combinations of three positions × 4³.

2. **Individual Action Model**
   - Action space: Moving up, down, left, or right for a single agent.
   - State-Action space: All possible combinations of three positions × 4.

3. **Stage Aware Shared Action Model**
   - State space includes stage information from the Series of Goals Environment.
   - Action space: Moving up, down, left, or right for all agents.
   - State-Action space: All possible combinations of three positions × number of stages × 4³.

---

## Results

The results demonstrate that the Q-Learning agents successfully learned to navigate towards the target position while minimizing collisions. The epsilon-greedy strategy allowed the agents to balance exploration and exploitation effectively.

### Single Goal Environment

#### Shared Action Model

- **Early Training (up to 10,000 episodes)**: The agents did not learn to avoid collisions.
- **Intermediate Training (100,000 episodes)**: The model consistently reached the goal with random initial positions but not always using optimal paths.
- **Advanced Training (1,000,000 - 1,500,000 episodes)**: Agents began to exhibit strategic behavior to avoid collisions and optimize pathfinding, although suboptimal behaviors persisted.

**Mean Rewards for Shared Action Model**:

| Episodes         | Mean Reward  |
|------------------|--------------|
| 100              | -8,692.27    |
| 10,000           | -7,258.21    |
| 100,000          | 4,961.25     |
| 1,000,000        | 8,652.79     |
| 1,500,000        | 8,954.06     |

#### Individual Action Model

- **Early Training**: Early episodes showed promising results with optimal paths and some collisions.
- **Intermediate Training (10,000 episodes)**: Agents began avoiding previously problematic paths, potentially preventing the model from learning the optimal policy.
- **Advanced Training**: Confusion arose in the model's responses due to inconsistent rewards, leading to fluctuating performance.

**Mean Rewards for Individual Action Model**:

| Episodes         | Mean Reward  |
|------------------|--------------|
| 100              | 4,971.75     |
| 10,000           | 7,086.28     |
| 100,000          | 7,350.91     |
| 1,000,000        | 6,691.43     |
| 1,500,000        | 6,629.37     |

### Series of Goals Environment

#### Shared Action Model

- Despite initial assumptions, the model consistently reached the third goal after 1,000,000 episodes, suggesting the existence of an optimal policy under inconsistent reward conditions.
  
**Mean Rewards for Shared Action Model**:

| Episodes         | Mean Reward     |
|------------------|-----------------|
| 100              | -8,650.29       |
| 1,000            | -8,589.93       |
| 100,000          | 6,813.36        |
| 1,000,000        | 107,415.86      |
| 1,500,000        | 107,405.01      |

#### Stage Aware Shared Action Model

- Incorporating stage information into the state space led to more stable learning outcomes and accelerated the learning process.
- The model consistently reached the last goal from as early as the 100,000th episode.
  
**Mean Rewards for Stage Aware Shared Action Model**:

| Episodes         | Mean Reward     |
|------------------|-----------------|
| 100              | -8,628.58       |
| 1,000            | -8,299.13       |
| 100,000          | 84,168.97       |
| 1,000,000        | 116,882.68      |
| 1,500,000        | 118,071.14      |

---

## Conclusion

This research has effectively demonstrated the application of Q-Learning to autonomous navigation within grid environments, showcasing its viability in scenarios involving multiple agents and dynamic objectives. The models developed adeptly learned to navigate towards goals while minimizing collisions, illustrating the robustness of Q-Learning in complex, multi-agent settings.

The results validate the effectiveness of the basic Q-Learning model and highlight potential improvements achievable through modifications like the incorporation of stage awareness, which significantly enhanced performance by providing a consistent reward system.

---

## References

<a name="references"></a>

[1] Devaraju, S., Ihler, A., & Kumar, S. (2023). *A Deep Q-Learning based, Base-Station Connectivity-Aware, Decentralized Pheromone Mobility Model for Autonomous UAV Networks*. arXiv preprint arXiv:2311.16409.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- Gratitude to Alexander Ihler who contributed insights and support during the development of this work.
- Appreciation to the University of California, Irvine, for providing resources and a conducive environment for research.

---