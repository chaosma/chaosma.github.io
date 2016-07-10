---
layout: post
title: Reinforcement learning on Tic-Tac-Toe 
description: 
headline: 
categories: AI
tags: 
  - AI
  - reinforcement_learning
comments: true
mathjax: true
featured: false
published: true
---
Tic tac toe is a simple game, but it's a good illustration for the reinforcement learning algorithm. I compared two algorithms: epsilon greedy algorithm and first visit Monte Carlo(FSMC) method. 

In Sutto's book, Chapter 1 introduced the epsilon greedy algorithm to learn the tic tac toe game. The agent contains a lookup table that for each state, it initially assigns a value that 1 for win state, 0 for draw state, -1 for loss state, 0.5 for otherwise. The epsilon greedy means for every move, the agent choose the maximum-value move(greedy) with probability 1-epsilon and random move(exploratory) with probability epsilon. The agent updates its value lookup table after each episode(game) using the following equation:

$$ V(s) \leftarrow (1-\alpha)*V(s) + \alpha*V(s')$$


This algorithm use the state after a move to update the state before the move. Thus the value of the states will be back traced from the ending state(win,lose,draw). However, the training speed of this algorithm is slow. Another way is to using the returns of each episode to update the state value instead of the next state. I trained the epsilon greedy agent and FSMC agent with random player with 200000 episodes, and for both situations i.e. the agent play first or second. Then I measured the wining rate for them. Here is the result:


    FSMC play first:

    FSMC win | epsilon greedy win   | draw
    0.8987   | 0.0290              | 0.0723


    epsilon greedy play first:

    epsilon greedy win | FSMC win | draw
    0.0317             | 0.8068   | 0.1615

As we can see, the FSMC has a much higher winning rate comparing with epsilon greedy. I uploaded the code to my github for reference.


