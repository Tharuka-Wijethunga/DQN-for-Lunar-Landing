# Deep Q-Learning for Lunar Landing

## Overview
This project implements a Deep Q-Learning algorithm to solve the Lunar Lander environment from the OpenAI Gymnasium. The environment is a classic rocket trajectory optimization problem, where the goal is to land a rocket safely on a landing pad.

## Environment Description

### Action Space
The action space consists of four discrete actions:
- `0`: Do nothing
- `1`: Fire left orientation engine
- `2`: Fire main engine
- `3`: Fire right orientation engine

### Observation Space
The state is represented by an 8-dimensional vector containing:
- The lander's coordinates (x, y)
- The lander's linear velocities (x, y)
- The lander's angle
- The lander's angular velocity
- Two booleans indicating whether each leg is in contact with the ground

### Rewards
The rewards are structured as follows:
- Increased/decreased the closer/further the lander is to the landing pad.
- Increased/decreased the slower/faster the lander is moving.
- Decreased the more the lander is tilted.
- Increased by 10 points for each leg in contact with the ground.
- Decreased by 0.03 points each frame a side engine is firing.
- Decreased by 0.3 points each frame the main engine is firing.
- Additional reward of +100 for landing safely, -100 for crashing.

### Episode Termination
An episode terminates when:
- The lander crashes.
- The lander goes outside the viewport.
- The lander is not awake.

## Implementation

### Neural Network
A neural network is implemented using PyTorch with the following architecture:
- Input layer: Size equal to the state size (8).
- Two hidden layers: Each with 64 units and ReLU activation.
- Output layer: Size equal to the action size (4).

### Experience Replay
Experience replay is implemented to store and sample past experiences to break the correlation between consecutive experiences and stabilize training.

### DQN Agent
The DQN agent is responsible for:
- Selecting actions using an epsilon-greedy policy.
- Storing experiences in replay memory.
- Sampling experiences and learning from them.
- Performing soft updates on the target network to ensure stable training.

### Hyperparameters
The following hyperparameters are used:
- `learning_rate = 5e-4`
- `minibatch_size = 100`
- `discount_factor = 0.99`
- `replay_buffer_size = 1e5`
- `interpolation_parameter = 1e-3`
- `number_episodes = 2000`
- `maximum_number_timesteps_per_episode = 1000`
- `epsilon_starting_value = 1.0`
- `epsilon_ending_value = 0.01`
- `epsilon_decay_value = 0.995`
