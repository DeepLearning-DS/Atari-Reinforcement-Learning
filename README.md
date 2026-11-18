
# Atari-Deep-Reinforcement-Learning-


I have tried to implement the algorithm(Deep Q-learning with Experience Replay) given in this novel paper.
Paper Link - https://arxiv.org/pdf/1312.5602.pdf

I have added the folder of weights, please do consider evaluating them.

# Deep Q-learning with Experience Replay :
Its really not possible to use a simple Q-table for training games like chess,mario or breakout unless we have a memory size which can handle a state-space of order 10^100 and a super computer to speed up computations. To avoid this problem,I used a Deep Q network(DQN) approximating Q(s, a) value.

To approximate the next Q value, which would be required to train the policy network, made a clone of the policy network called the Target Network. To this target network,passed the state of game that is reached due to the action dictated by the policy network's output, i.e, the Q values. Taking this state as input, the target network generates the Q-values for next action.

![DQN](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning-/blob/master/Assets/Others/DQN_Algorithm.png)

![CNN](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning-/blob/master/Assets/Others/CNN.png)

With both experience replay and the target network, here's a more stable input and output to train the network and behaves more like supervised training.

This is the 4 layer CNN architecture used in the paper. I have used the same architecture to train agent in this project.

# Implementation Details :
Have have used Keras for all implementations and Matplotlib to visualize the graphs for rewards and losses to implement the same alogrithm mentioned above. I had previously trained using both optimizers - RMSProp and Adam. Adam worked better for this implementation. Replay Memory Size was fixed at 40000 experiences because of ram limitations. Before training, initial exploration is done to gain some random experiences and fill up replay memory. this implementation can be used to train any atari game. Trained **Breakout** and **SpaceInvaders** in a deterministic enviroment using OpenAI Gym library. After training for _ episodes, start getting satisfying results. Training for SpaceInvaders is still in progress but I hope to complete it soon with good results.

# Results from our experiments :

![Breakout avg](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/Assets/Results/Breakout%2050%20Avg.png)

![Breakout score](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/Assets/Results/Breakout%20Score.png)

![SpaceInvaders avg](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/Assets/Results/SpaceInvaders%20Avg%2010.png)

![SpaceInvaders score](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/Assets/Results/SpaceInvaders%20Score.png)

# Issues Commonly facesd :

* I needed to take care of some issues in games like Breakout where fire has to be pressed manually after losing a life. This is done because the Q-value of "fire" becomes very less and it is very hard to determine those 5 occurences(5 Lives) of pressing fire. There is a similar problem in Pong as well.

* Initially in Breakout, agent was getting decent score but it was because this agent was getting stuck at local minima. The Slider moved to the extreme of the frame to gain some initial advantage but was getting stuck there.

# Instructions to Run :

* pip install -r requirements.txt
* Before training, make sure you set the [hyperparameters](https://github.com/geeky-wizard/Atari-Deep-Reinforcement-Learning/blob/master/hyperparameters.py) correctly.
* python main.py GAME_NAME (By default, breakout is loaded and games are loaded in a deterministic enviroment(v4))
* Choose among the options : 1 for train, 2 for test, 3 for seeing results on our pretrained weights(Log files are used for this purpose).
* When training for first time, initial exploration will be done first and then training. User has to manually enter the number of episodes he want to train the agent.
* All weights,experiences,logs and results can be found in the Assets folder.
