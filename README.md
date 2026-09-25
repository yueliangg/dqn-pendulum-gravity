# DQN Pendulum Control Under Different Gravity Conditions

## Overview

This project applies Deep Q-Learning (DQN) to the `Pendulum-v0` environment to investigate how different gravity conditions affect learning and control behaviour.

The project also evaluates whether systematic hyperparameter tuning can improve learning performance and stability, and compares the trained DQN against simple non-learning control baselines.

## Objectives

- Apply Deep Q-Learning to the Pendulum control problem.
- Convert continuous torque control into a discrete action space.
- Compare DQN performance under different gravity conditions.
- Analyse control behaviour using angle, angular velocity and torque.
- Systematically tune key DQN hyperparameters.
- Validate the selected configuration across multiple training seeds.
- Compare DQN performance with Random, Zero-Torque and heuristic controllers.

## Environment

- **Environment:** Pendulum-v0
- **Framework:** TensorFlow
- **Language:** Python
- **Action space:** 9 discrete torque actions from -2 to 2
- **DQN architecture:** 3 → 128 → 128 → 9
- **Discount factor:** 0.99
- **Replay buffer:** 50,000
- **Batch size:** 64

## Experiments

### 1. Gravity Comparison

The DQN was evaluated under four gravity settings:

| Gravity | Mean Evaluation Reward |
|---|---:|
| Free-fall (0) | -54.21 |
| Anti-gravity (-10) | -62.53 |
| Default (10) | -192.28 |
| Supergravity (15) | -305.38 |

The results show that the gravity setting substantially affects control difficulty and behaviour. Supergravity produced larger angular velocity changes and greater control instability, while free-fall and anti-gravity produced more favourable rewards.

### 2. Hyperparameter Tuning

Key DQN settings were systematically evaluated, including:

- Learning rate
- Target network update frequency
- Epsilon decay
- Action-space resolution

The selected configuration was:

| Parameter | Selected Value |
|---|---:|
| Learning rate | 0.00025 |
| Target update frequency | 10 |
| Epsilon decay | 0.99 |
| Number of actions | 9 |

The selected epsilon decay produced a modest improvement in final evaluation reward, while providing faster learning and more stable late-training behaviour.

### 3. Repeated-Seed Validation

The selected epsilon decay was evaluated across three training seeds to examine whether the observed improvement was consistent across different training runs.

### 4. Non-Learning Baselines

The trained DQN was compared against:

- Random Policy
- Zero-Torque Policy
- Simple Heuristic Controller

These comparisons provided reference points for evaluating whether the learned policy performed better than simple control strategies.

## Behaviour Analysis

DQN behaviour was analysed using:

- Angle over time
- Angular velocity over time
- Torque over time
- Episode animations

These visualisations were used to interpret how the agent responded to different gravity conditions rather than relying only on reward values.

## Key Findings

- Gravity strongly affected both reward and control behaviour.
- Supergravity was the most challenging tested condition for the DQN.
- The selected epsilon decay improved learning speed and late-training stability.
- The improvement in final default-gravity evaluation reward was relatively modest.
- The DQN outperformed the tested non-learning baselines in mean evaluation reward across the four gravity conditions.
- Nine discrete actions provided better greedy evaluation performance and late-training stability than the five-action sensitivity check.

## Limitations

- Training and evaluation were conducted using the tested environment and selected experimental settings.
- Repeated-seed validation used three training seeds.
- The gravity experiments used the selected configuration without separately tuning the DQN for each gravity condition.

## Tools & Technologies

**Python · TensorFlow · NumPy · OpenAI Gym · Deep Learning · Reinforcement Learning · Data Analysis**

## Files

- `ca2_partb.ipynb` — Main project notebook
- `report.pdf` — Project report
- `figures/` — Selected experiment visualisations
