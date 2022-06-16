## Udacity Deep Reinforcement Learning Nanodegree 
## Project 3: Collaboration and Competition

### Learning Algorithm

In this project I again used the Deep Deterministic Policy Gradients algorithym from the previous project and extended it to train multiple agents from the same learning experience (MADDPG). Deep Deterministic Policy Gradients Method is classified as an actor-critic method 
In solving this environment, I started with the code implementation example in the course lab and modified them to solve the tennis environment.  
MADDPG trains actors and critics using all agents information (actions and states). However, the trained agent model (actor) can make an inference independentaly using its own state.
Noise based on an Ornstein-Uhlenbeck process is added to the predicted actions to encourage exploration.

### Deep Network Architecture

The actor network of each agent has 3 fully connected layers with 256 units in the first hidden layer and 128 units in the second hidden layer.  ReLu activation functions are used in the first two layers and tanh function in the third layer. 

The critic network has also 3 fully connected hidden layers with 256 units in the first hidden layer 128 units in the second hidden layer. ReLu activation functions are used in the first two layers and tanh function in the output layer. 

#### Hyperparameters

- `BUFFER_SIZE = 10000` is the number of experience tuples `(state, action, reward, next_state, done)` that are stored in the replay buffer and avaiable for learning
- `BATCH_SIZE = 256` is the number of tuples that are sampled from the replay buffer for learning, i.e. the minibatch size.
- `GAMMA = 0.99` is the discount factor that controls how far-sighted the agent is with respect to rewards. `GAMMA = 0` implies that only the immediate reward is important and `GAMMA = 1.0` implies that all rewards are equally important, irrespective whether they are realised soon and much later
- `TAU = 0.001` controls the degree to which the target Q-network parameters are adjusted toward those of the local Q-network. `TAU = 0` implies no adjustment (the target Q-network does not ever learn) and `TAU = 1` implies that the target Q-network parameters are completely replaced with the local Q-network parameters
- `LR_ACTOR' = 0.0001` is the learning rate for the gradient ascent update for the actor network. 
- `LR_CRITIC' = 0.0003` is the learning rate for the gradient ascent update for the actor network. 
- `WEIGHT_DECAY=0` L2 weight decay.


#### Results

The environment is solved by reaching +0.516 average scores over 100 episodes (taking the maximum of two agents) after 1178 episodes. The accumulation of rewards are given in the figure below:

![results](https://user-images.githubusercontent.com/66205537/174100186-64a2e883-cc0e-43b3-a5c2-431537a0fe75.png)

From the figure, it is seen that the learning of the agent continuously improves. I interrupted the training as the episodes take very long time since the agents play well and keep the ball in the game. 

#### Future Improvements

Although the results are quite satisfactory they can still be improved :
1. I observed that the training performance of the agents were highly sensitive, i.e. when I run the code several times with the same hyperparameters I got different results. For some cases the agents could not get a score higher than 0.1 while in some cases they managed to get 0.5. This is one target for myself to improve my code to get more consistent results among multiple runs.
2. I also observed the performance of the agent suddenly drops after a certain peak, wihch may be termed as instability. Further variation of hyperparamters can be tried to eliminate this affect. 
3. Alternative learning algorithyms like DDPG with centralized training and decentralized execution can also be tried.  
