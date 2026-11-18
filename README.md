
# Atari-Deep-Reinforcement-Learning-


I have tried to implement the algorithm(Deep Q-learning with Experience Replay) given in paper Playing Atari with Deep Reinforcement Learning, published by brilliant Ioannis Antonoglou while he was at DeepMind Technologies along with his Team.

Paper Link - https://arxiv.org/pdf/1312.5602.pdf

I have added the folder of weights, please do consider evaluating them.

# Deep Q-learning with Experience Replay :
Its really not possible to use a simple Q-table for training games like Chess,Mario or Breakout unless we have a memory size which can handle a state-space of order 10^100 and a super computer to speed up computations. To avoid this problem,I used a Deep Q network(DQN) approximating Q(s, a) value.

To approximate the next Q value, which would be required to train the policy network, made a clone of the policy network called the Target Network. To this target network,passed the state of game that is reached due to the action dictated by the policy network's output, i.e, the Q values. Taking this state as input, the target network generates the Q-values for next action.

![DQN] <img width="645" height="361" alt="DQN_Algorithm" src="https://github.com/user-attachments/assets/42d373f5-a5fe-4b97-ba3c-06bda86326cc" />

![DQN Formula] <img width="639" height="44" alt="DQN_Formula" src="https://github.com/user-attachments/assets/90eea110-7f2e-480e-9d82-3cf357b69ab5" />

 
![CNN] <img width="674" height="243" alt="CNN(1)" src="https://github.com/user-attachments/assets/fb521ef3-3cfd-41ea-886e-db9e9ff0a360" />


With both experience replay and the target network, here's a more stable input and output to train the network and behaves more like supervised training.

This is the 4 layer CNN architecture used in the paper. I have used the same architecture to train agent in this project.

# Implementation Details :
Have have used Keras for all implementations and Matplotlib to visualize the graphs for rewards and losses to implement the same alogrithm mentioned above. I had previously trained using both optimizers - RMSProp and Adam. Adam worked better for this implementation. Replay Memory Size was fixed at 40000 experiences because of ram limitations. Before training, initial exploration is done to gain some random experiences and fill up replay memory. this implementation can be used to train any atari game. Trained **Breakout** and **SpaceInvaders** in a deterministic enviroment using OpenAI Gym library. After training for _ episodes, start getting satisfying results. Training for SpaceInvaders is still in progress but I hope to complete it soon with good results.

# Results from our experiments :

![Breakout avg] <img width="1920" height="1440" alt="Breakout 50 Avg" src="https://github.com/user-attachments/assets/4375b78d-6551-494a-95a1-f032b4a79e3a" />


![Breakout score] <img width="1920" height="1440" alt="Breakout Score" src="https://github.com/user-attachments/assets/5e0411ce-72cd-4bca-8546-c24b192e78ee" />


![SpaceInvaders avg] <img width="1920" height="1440" alt="SpaceInvaders Avg 10" src="https://github.com/user-attachments/assets/e83e3946-9070-4939-8b8c-f39a1f6ad0b7" />


![SpaceInvaders score] <img width="1920" height="1440" alt="SpaceInvaders Score" src="https://github.com/user-attachments/assets/06a1ab0b-7e04-4bfc-8668-9ad5e7a86071" />

# Issues Commonly faced :

* I needed to take care of some issues in games like Breakout where fire has to be pressed manually after losing a life. This is done because the Q-value of "fire" becomes very less and it is very hard to determine those 5 occurrences(5 Lives) of pressing fire. There is a similar problem in Pong as well.

* Initially in Breakout, agent was getting decent score but it was because this agent was getting stuck at local minima. The Slider moved to the extreme of the frame to gain some initial advantage but was getting stuck there.

# Instructions to Run :

* pip install -r requirements.txt
* Before training, make sure you set the [hyperparameters](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/hyperparameters.py) correctly.
* python main.py GAME_NAME (By default, breakout is loaded and games are loaded in a deterministic environment(v4))
* Choose among the options : 1 for train, 2 for test, 3 for seeing results on our pre-trained weights(Log files are used for this purpose).
* When training for first time, initial exploration will be done first and then training. User has to manually enter the number of episodes he want to train the agent.
* All weights,experiences,logs and results can be found in the Assets folder.
