# Project 1: Navigation

## Project Details
The goal of this project is to train an agent to navigate and collect bananas within a square environment using the DQN algorithm ([Deep Q-Network](https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf)).

![alt text](https://raw.githubusercontent.com/acampos074/Deep-Q-Network-Navigation/master/Figures/trained_agent.gif)

The agent receives a reward of +1 for every yellow banana and -1 for every blue banana that it collects. The goal is to collect the maximum amount of yellow bananas while avoiding the blue ones.

The state space has 37 dimensions, which contains the agent's velocity and ray-based perception of objects around the agent's forward direction. Each state space value ranges between 0 and 1. With this information the agent needs to learn the best four discrete actions:

* `0` - move forward
* `1` - move backward
* `2` - turn left
* `3` - turn right

The task is episodic, and to solve the environment the agent must get an average score greater than 13 over 100 consecutive episodes.

## Getting Started
You will need to set up your python environment.
1. Create (and activate) a new environment with Python 3.6.

    - __Linux__ or __Mac__: 
    ```bash
    conda create --name drlnd python=3.6
    source activate drlnd
    ```
    - __Windows__: 
    ```bash
    conda create --name drlnd python=3.6 
    activate drlnd
    ```
2. Perform a minimal install of [OpenAI](https://github.com/openai/gym) `gym` with:
```
pip install gym
```
  * Install the **classic control** environment group by following the instructions [here](https://github.com/openai/gym#classic-control)
  * Install the **box2d** environment group by following the instructions [here](https://github.com/openai/gym#box2d)
3. Clone the Udacity's Deep Reinforcement Learning repository
```
git clone https://github.com/udacity/deep-reinforcement-learning.git
cd deep-reinforcement-learning/python
pip install .
```
4. Create an [IPython kernel](https://ipython.readthedocs.io/en/stable/install/kernel_install.html) for `drlnd` environment
```
python -m ipykernel install --user --name drlnd --display-name "drlnd"
```
5. Before running code in a notebook, change the kernel to `drlnd` environment by using the drop-down `Kernel` menu.
6. For this project you will need to download the pre-built environment prepared by Udacity, and you can download it from one of the links below. You need to download the file that matches your operating system:

   - Linux: [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
   - Mac OSX: [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
   - Windows (32-bit): [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
   - Windows (64-bit): [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)

7. Download this repository within your working directory.

## Instructions

Follow the instruction in `Navigation.ipynb` to get started with training your agent!
## Files
* `Navigation.ipynb` This is the Jupyter notebook that contains the implementation of the DQN algorithm.
* `dqn_agent.py` This Python file contains two classes: `Agent` and `ReplayBuffer`. The `Agent` class contains an `act` method used to return an action for a given state and current policy. It also has a `learn` method used to updated the Q-network parameters given a batch of experience tuples. The `ReplayBuffer` class has an `add` method to add a new experience to the memory buffer, and a `sample` method used to randomly fetch a batch of experiences from memory.
* `model.py` This Python file contains the Q-Network model, which maps 37 input states to 4 action values. This neural network contains two hidden layers, each with 64 nodes. A ReLU activation function is used after the output of the first and second hidden layers, and an identity activation function for the output.
* `checkpoint.pth` This file contains the DQN weights of the trained agent.


## License
The source code is released under an [MIT license.](https://opensource.org/licenses/MIT)
## Acknowledgements
I would like to thank the Udacity community for the technical support and for providing coding exercises that helped me understand the implementation of this algorithm.

## Author
Andres Campos
