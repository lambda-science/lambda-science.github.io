---
title: Hide and Seek AI with Deep Reinforcement Learning
description: How to train an AI agent that play hide and seek in a random 2D map
date: 2023-09-02
authors:
  - corentin
categories:
  - Blog Post
draft: false
---

# Hide and Seek AI agent with Deep Reinforcement Learning

_A simple introduction to deep reinforcement learning and how I trained an AI agent that play hide and seek in a random 2D map_

<!-- more -->

---

In this small blog post, I'm going to show you how I coded an AI that is able to play hide and seek in a 2D map. Here is what it looks like in the end:

![https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/ppo_random.gif](https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/ppo_random.gif)

## What's Reinforcement Learning

Let's start with the basics of reinforcement learning. Contrary to supervised learning where you have a dataset that you learn on, in **reinforcement learning** you don't have a pre-existing dataset, you have an **environment**. Reinforcement learning is used for iterative tasks such as playing chess for example or teaching a robot how to walk.

Your AI model called an **agent** is going to learn by exploring this environment by taking **action**. For each action performed, the agent will get a reward (or penalty) to indicate if it was a good action or not, to learn what we call a **policy**. The end goal of the AI agent is to **maximize his rewards** by learning an efficient policy.

The cooking recipe for a reinforcement learning task:

- an **environment**, created here using `gymnasium` python library.
- a set of **actions** (defined by the environment) and observation space (what information has the agents to decide on the action, defined by the environment)
- a **reward function** with an end goal (winning, hiding, defined by the environment)
- a training algorithm to learn a **policy** such as Deep Q-Learning, here using `Stable-Baselines3` python library.

## Problem Description & AI Goal

In this project we want to create an AI model that is able to hide in a 2D map. The guard (player) is placed randomly and the AI model needs to move to find a good hiding spot. What is a good hiding spot you're going to ask, I have defined it as such: **good hiding spots** are the **3 tiles** from the map that are the **furthest away** from the guard, with **no direct line of sight** from the guard and that has at **least 2 adjacent obstacles.**

If we take our recipe here is what it looks like:

- environnement: a 12x12 2D matrix with 3 to 4 randomly placed obstacles, a randomly placed guard and our randomly placed agent
- actions & observation space: moving up down left and right, the agent has access to all (part 1) or partial (part 2) information (all elements positions)
- reward: +1 if reaching a good hiding spot

## Pre-determined map with custom environment and Deep Q-Learning (DQN)

In this first iteration, I decided to start small. I created my own gym environment with the official documentation, in which the map is predefined by hand with 4 main obstacles and the agent has access to all information about the current state of the environment.

I trained an AI model with the DQN algorithm using the `MlpPolicy` for 20M time steps (actions), and a high exploration rate (more information in the repository). Here is what the training curves looks like ([full logs](https://tensorboard.dev/experiment/71F5RvkkRO6lu03eC7y6gg)):

![https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/image-1.png](https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/image-1.png)

On the right we have the mean rewards over all training steps, we see that our agent is always capable of finding a good hiding spot (success when reward = 1). On the left we have the mean number of steps taken by our agent to find a good hiding spot. We can see that it decreases overtime to reach a minimum of around 8 steps. This means that during training our agent is more and more efficient at finding a good hiding spot fast.

Here is our trained agent solving the environment:

![https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/dqn_determinist.gif](https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/dqn_determinist.gif)  
Blue is our agent, red is the guard, green is good hiding spots, black are pillars.

This works very well on a predefined map, however, there are two issues: (i) the training takes a long time, 20M steps took around 10h to reach (ii) when training on random map the agent is not capable of finding good hiding spots, the average number of steps to reach the spots does not decrease.

## Random map with Minigrid env and PPO algorithm

To solve previous issues we changed two things: (i) we used a new environment called MiniGrid that I modified for this project (ii) we used a new training algorithm called PPO.

(i) The minigrid is similar to our previous environment, however, this environment in represented as an image (not a flat observation space) AND the agent only have access to a 6x6 square observation in front of him, not all the map.  
(ii) PPO uses a different training approach that in my experience has been proven more efficient in terms of performance and time.

So we trained this PPO model with the CNN policy (image) for 10M time steps (actions), and a high exploration rate on this new Minigrid random map environment (more information in the repository).

Here is what the training curves looks like ([full logs](https://tensorboard.dev/experiment/71F5RvkkRO6lu03eC7y6gg)):

![https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/image-4.png](https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/image-4.png)

Way noisier than before BUT at least we can see that the mean reward is very close to 1 and that the average number of steps to find a good hiding spots decrease over time to reach around 18 in the final model state. The number of steps is slightly higher than before because in this environment there is more action, the agent has to turn on himself to move.

Here is our trained agent solving our new random environment (orange lava represents the guard player):

![https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/ppo_random.gif](https://raw.githubusercontent.com/lambda-science/jumbo-tech-test/main/readme_assets/ppo_random.gif)

**And with that we just trained an AI model capable of playing hide and seek in a random map environment using deep reinforcement leaning ! 🥳**

If you want more information about this, you can check out [my repository with the code](https://github.com/lambda-science/jumbo-tech-test) and a more detailed Readme. You can also follow me on twitter to keep you updated on my posts: [@corentinm_py](https://twitter.com/corentinm_py)
