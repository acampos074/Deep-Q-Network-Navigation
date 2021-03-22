## Report
### Learning algorithm
The algorithm used to solve this Reinforcement Learning problem is Deep Q-Learning (DQN). In this algorithm, an agent is trained for a fixed number of episodes, and for a fixed episode length. For each episode, the agent observes the current state, then chooses an action derived from an epsilon-greedy policy and sends it to the environment. Afterwards, the environment provides a reward and an updated state to the agent. Fig. 1 provides an illustration of this algorithm. Note, that initially the algorithm starts with an epsilon value of 1 (i.e. the agent initially takes random actions). As the agent goes through more training episodes this epsilon decreases and starts taking more actions using the Q-network. 

![alt-text](https://raw.githubusercontent.com/acampos074/Deep-Q-Network-Navigation/master/Figures/DQN.png)

**Figure 1 | Schematic illustration of the DQN algorithm.** DQN takes the state as input and returns a corresponding predicted action for an epsilon-greedy action selection policy.   

This algorithm uses neural networks (Q-networks) to generate a nonlinear function approximation of the action-value function. Fig. 2 illustrates the architecture implemented in this project.

![alt-text](https://raw.githubusercontent.com/acampos074/Deep-Q-Network-Navigation/master/Figures/nn.png)

**Figure 2 | Schematic illustration of the neural network architecture.** The input to the neural network consist of a 37x1 tensor of states, followed by two fully connected hidden layers each with 64 nodes. The output layer consist of a 4x1 tensor of actions. Each hidden later is followed by a rectified linear unit (ReLU) activation function.

The algorithm has two Q-netwoks (local and target). The weights of the target Q-network are determined by minimizing the following loss function:

![alt-text](https://raw.githubusercontent.com/acampos074/Deep-Q-Network-Navigation/master/Figures/loss_function.png)

Where (s,a,r,s')~U(D) are minibatches of experiences drawn from a uniform random distribution from the replay memory buffer, &gamma; is a discount factor, Q(s,a;&theta;<sub>i</sub>) is the expected Q values from the local model, and r+&gamma;maxQ(s',a';&theta;<sub>i</sub><sup>-</sup>) is the Q target for the current states. These weights are updated every four steps, and held constant for individual steps.

This algorithm uses two key ideas:

* Experience Replay
* Fixed Q-Targets

Experience replay helps to break correlations from sequential observations. During training, a set of random experiences from the memory buffer and these are used to break these correlations. Fixed Q-Targets helps to break correlations with the targets (i.e. it helps solve the problem of training with a moving target). Thus, the target Q-Network's weights are updated less often than the weights of the local Q-network. Table 1 includes the hyperparameters used in this implementation.

#### **Table 1 | List of hyperparameters and their values**
| **Hyperparameter**      | **Value** | **Description**     |
| :---        |    :---   |  :--- |
| `BUFFER_SIZE`      | 100000       | Size of the replay memory buffer. [Adam algorithm](https://arxiv.org/abs/1412.6980) (a variant of stochastic gradient decent (SGD) algorithm) updates are sampled from this buffer.    |
| `BATCH_SIZE`   | 64        | Number of training cases used to compute each SGD update.      |
| `GAMMA`   | 0.99        | Gamma is the discount factor used in the Q-learning update.     |
| `TAU`   | 0.001  |  Tau is an interpolation parameter used to update the weights of the Q-target network |
| `LR`   | 0.0005  |  Learning rate used by the Adam algorithm.  |
| `UPDATE_EVERY`   | 4  | The number of actions taken by the agent between successive SGD updates.  |
| `eps_start`  | 1.0  |  Starting value of &epsilon; for &epsilon;-greedy action selection.   |
| `eps_end`   |  0.01 |  Minimum value of &epsilon; for &epsilon;-greedy action selection. |
|`eps_decay`   | 0.995  | Multiplicative factor to decrease &epsilon; per episode.  |

Fig. 3 illustrates the temporal evolution of the agent's score-per-episode.

![alt-text](https://raw.githubusercontent.com/acampos074/Deep-Q-Network-Navigation/master/Figures/avg_scores.png)
**Figure 3 | Training curve tracking the agent's score.** The average scores (orange line) shows that the agent is able to receive a score of at least +13 over 500 episodes.
### Ideas of Future Work
Other ideas to further improve the agent's performance include:
* Double DQN
* Prioritized Experience Replay
* Dueling DQN
