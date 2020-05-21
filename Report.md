

- to Blve the environment, the agents must get an average score of +0.5 over 100 consecutive episodes, 
after taking the maximum over both agents. Algorithms and Techniques 

To train the Tennis agents I used MDDGP algorithm implementing centralized training and decentralized execution. 
Each agent receives its own, local observation. 

Thus it will be possible to simultaneously train both agents through self-play. 

During training, the critic for each agent uses extra information like states observed and actions taken by all other agents.

For the actor, there is one for each agent. 

Each actor has access to only its agents observations and actions. 

During execution time only actors are present and all observations and actions are used. 

MADDPG (Multi-agent DDPG) class uses 2 DDPG agents similar to what was used in Udacity classroom 
for previous projects. Also ReplayBuffer is used as a shared buffer between agents. 

MADDPG combines states, actions, rewards, next_states, dones from both agents and adds 

them to shared ReplayBuffer. MADDPG act calls act for 2 DDPG agents. The Actor network consists of 3 

linear layers. The first 2 linear layers are followed by Relu layer and the 3rd linear layer is followed by a Tanh 
layer as output layer. The sizes for the layers are 24 200, 200*150 and 150*2 respectively. 

The Critic has a similar structure with sizes of 52*200, 200*150 and 150*1. 

- Environment was solved in 2186 

episodes and the network weights for 2 agents were saved as agent1_checkpoint_actor.pth, 

agent1_checkpoint_critic.pth, agent2_checkpoint_actor.pth and agent2_checkpoint_critic.pth. 

For different trials the number of episodes to solve the environment was usually around 2000.


Trained Models

- The agent1_checkpoint_actor.pth file represents the first agent actor
- The agent1_checkpoint_critic.pth file represents the first agent critic
- The agent2_checkpoint_actor.pth file represents the second agent actor
- The agent2_checkpoint_critic.pth file represents the second agent critic

# Further Improvements

The following techniques can be tried out to further improve the performance of the network

- Prioritized Experience Replay: This technique prioritizes the experiences and chooses the best experience for further training when sampling from the buffer. This is known to reduce the training time and make the training more efficient.
- Asynchornous Actor Critic Agent: This technique trains multiple worker agents that interact with a glocal network asynchronously to optimize the policy and value function. This way, each of these agents interacts with it’s own copy of the environment at the same time as the other agents are interacting with their environments.
- Proximal Policy Optimization: This technique modifies the parameters of the network in such a way that the new set of parameters is looked for in the immediate neighbourhood of the parameters in the previous iteration of the training. This is shown also to be an efficient way of training the network so the search space is more optimal.
