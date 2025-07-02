---
title: "Sutton의 RL 책 한 장 요약"
date: 2025-06-15T11:30:03+00:00
weight: 1
# aliases: ["/first"]
tags: ["RL"]
author: "mori"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "한 페이지로 보는 Sutton의 RL 책"
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
math: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/moripiri/moripiri.github.io/issues"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
**Reinforcement Learning: An Introduction** by Richard S. Sutton and Andrew Barto: [link](https://www.andrew.cmu.edu/course/10-703/textbook/BartoSutton.pdf)
<!--more-->

## Reinforcement Learning
An area of machine learning that aims to learn what to do to

### Agents and Environments

<p align="center">
 <img src = "images/agent_environment.png">
</p>

At each timestep $t$ 
*  **Agents**: Receives Reward $R_t$ and Observation $O_t$, executes Action $A_t$
* **Environments**: Receives Action $A_t$, then emits Reward $R_{t+1}$ and Next Observation $O_{t+1}$ 

The sequence of observations, actions, rewards are called history.</br>

$$\begin{align}
H_t = O_1, R_1, A_1, ... , A_{t-1}, O_t, R_t
\end{align}$$
</br>
</br>
**State**$(S_t)$: information used to determine what happens next. Both agent and environment have state, and it may not agree with each other

* **Fully observable environments**: $O_t = S_t$. Agent can know exact state of the environment. It is called **markov decision process (MDP)**
* **Partially observable environments**: $O_t \neq S_t$. Agent only know partial state of the environment. It is called **partially observable markov decision process (POMDP)**


### Markov Decision Processes (MDP)

**Markov Decision Process (MDP)** is an environment that can be defined as 5-tuple:

$$\begin{align}
(\mathcal{S}, \mathcal{A}, \mathcal{P}, \mathcal{R}, \gamma)
\end{align}$$

where

- $\mathcal{S}$: state space (set of states)

- $\mathcal{A}$: action space (set of actions)

- $\mathcal{P}$: state transition probability matrix $\mathcal{P}=\mathbb{P}[S_{t+1}=s'|S_t=s, A_t=a]$

- $\mathcal{R}$: reward function $\mathcal{R} = \mathbb{E}[R_{t+1}|S_t=s, A_t=a]$

- $\gamma$: discount factor $\gamma \in [0, 1]$

#### Markov Property

$$\begin{align}
\mathbb{P}[S_{t+1}|S_t] = \mathbb{P}[S_{t+1}|S_1, S_2, ... , S_t]
\end{align}$$

#### Policy

$$\begin{align}
\pi(a|s) = \mathbb{P}[A_{t} = a|S_t = s]
\end{align}$$

#### Return

$$\begin{align}
G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} \cdots  = \sum_{k=0}^\infty \gamma^k R_{t+k+1}
\end{align}$$

where $\gamma \in [0, 1]$

#### Value function & Action-value function (Q-value function)

$$\begin{align}
v_\pi(s) = \mathbb{E}_\pi[G_t|S_t = s]
\end{align}$$

$$\begin{align}
q_\pi(s, a) = \mathbb{E}_\pi[G_t|S_t = s, A_t = a]
\end{align}$$

#### Bellman equation

Let’s derive the Bellman expectation equation for $v_\pi(s)$.

$$
\begin{aligned}
v_{\pi}(s) &= \mathbb{E}_{\pi}[G_t \mid S_t = s]  \\
        &= \mathbb{E}_\pi \left[\sum_{k=0}^\infty \gamma^k R_{t+k+1} \mid S_t = s \right]  \\
        &= \mathbb{E}_\pi \left[R_{t+1} + \gamma \sum_{k=0}^\infty \gamma^k R_{t+k+2} \mid S_t = s \right]  \\
        &= \mathbb{E}_\pi \left[R_{t+1} + \gamma v_\pi(s_{t+1}) \mid S_t = s \right]
\end{aligned}
$$

$$
\begin{aligned}
q_\pi(s, a) &= \mathbb{E}_\pi[R_{t+1} + \gamma q_\pi (S_{t+1}, A_{t+1}) \mid S_t = s, A_t = a]
\end{aligned}
$$
