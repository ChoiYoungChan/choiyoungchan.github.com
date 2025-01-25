---
title:  "[AI] 강화학습(Reinforcement Learning)의 기본 개념 정리(Python 샘플코드 포함)"
excerpt: Artificial Neural Network

categories:
  - AI
tags:
  - [AI, 강화학습, Reinforcement Learning]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 강화학습(Reinforcement Learning)의 개념
---
강화 학습은 *에이전트(Agent)* 라는 주체가 *환경(Environment)* 과 상호작용하며 *보상(Reward)* 을 최대화하는 방향으로 학습하는 방식입니다. 마치 강아지 훈련과 비슷합니다. 강아지(에이전트)가 특정 행동(앉기)을 했을 때 간식(보상)을 주면, 강아지는 그 행동을 반복하게 됩니다. 반대로 잘못된 행동을 했을 때는 보상을 주지 않거나 벌을 주어 그 행동을 하지 않도록 학습시킵니다.

좀 더 학문적으로 표현하자면, 강화 학습은 에이전트가 환경의 상태(State)를 관찰하고, 주어진 상태에서 행동(Action)을 선택하며, 그 결과로 환경으로부터 보상(Reward)과 다음 상태(Next State)를 받는 과정을 통해 최적의 *정책(Policy)* 을 학습하는 것입니다. 정책은 주어진 상태에서 어떤 행동을 해야 보상을 최대화할 수 있는지에 대한 규칙 또는 전략입니다.
<br><br>


<img width="1120" alt="reinforcement-learning-figure" src="https://github.com/user-attachments/assets/1df53510-aea3-4632-bb0a-a25ce3d300fb" />
(출처 : https://www.ibm.com/think/topics/reinforcement-learning)<br><br>

### 강화 학습의 주요 구성 요소
---
* 에이전트 (Agent): 학습 주체. 환경과 상호작용하며 행동을 수행합니다.
* 환경 (Environment): 에이전트가 존재하는 세계. 에이전트에게 상태와 보상을 제공합니다.
* 상태 (State): 에이전트가 현재 처해 있는 상황. 에이전트는 환경을 관찰하여 현재 상태를 파악합니다.
* 행동 (Action): 에이전트가 환경에 대해 취할 수 있는 동작.
* 보상 (Reward): 에이전트의 행동에 대한 평가. 에이전트는 보상을 최대화하는 방향으로 학습합니다.
* 정책 (Policy): 주어진 상태에서 어떤 행동을 선택해야 하는지에 대한 규칙 또는 전략. 강화학습의 목표는 최적의 정책을 학습하는 것입니다.

<br><br>

### 강화 학습의 종류
---
강화 학습은 여러 가지 기준으로 분류할 수 있지만, 대표적인 분류는 다음과 같습니다.

* 모델 기반 (Model-Based) vs. 모델 프리 (Model-Free)
  * 모델 기반: 환경의 모델을 학습하여, 모델을 사용하여 미래의 상태와 보상을 예측합니다. 예측된 정보를 바탕으로 정책을 개선합니다.
  * 모델 프리: 환경의 모델을 학습하지 않고, 직접 환경과 상호작용하면서 얻은 경험을 통해 정책을 학습합니다.

* 가치 기반 (Value-Based) vs. 정책 기반 (Policy-Based)
  * 가치 기반: 각 상태 또는 상태-행동 쌍의 가치를 추정하여, 가치가 높은 행동을 선택하는 방식으로 학습합니다. Q-러닝, SARSA 등이 대표적인 알고리즘입니다.
  * 정책 기반: 정책을 직접 학습합니다. 정책을 나타내는 파라미터를 조정하여, 더 높은 보상을 얻을 수 있는 행동을 선택하도록 학습합니다. 정책 경사(Policy Gradient) 등이 대표적인 알고리즘입니다.

* On-Policy vs. Off-Policy
  * On-Policy: 현재 학습하고 있는 정책을 사용하여 행동을 선택하고 학습합니다. 즉, 경험을 생성하는 정책과 학습에 사용하는 정책이 동일합니다. SARSA가 대표적인 예입니다. 마치 자신이 운전하는 방식대로 운전 실력을 평가받는 것과 같습니다.
  * Off-Policy: 행동을 선택하는 정책과 학습에 사용하는 정책이 다릅니다. 다른 정책(예: 무작위 정책)으로 얻은 경험을 사용하여 현재 정책을 학습할 수 있습니다. Q-러닝이 대표적인 예입니다. 마치 다른 사람의 운전 경험을 보고 자신의 운전 실력을 향상시키는 것과 같습니다.
<br><br>

### 강화학습(Reinforcement Learning)의 과정
---
강화 학습은 시행착오(Trial and Error)를 통해 학습합니다. 에이전트는 다양한 행동을 시도해보고, 그 결과로 얻는 보상을 통해 어떤 행동이 좋은 결과를 가져오는지 학습합니다. 이 과정을 반복하면서 최적의 정책을 찾아나갑니다.

1. 환경 생성 (Environment Creation)<br>
강화학습을 위한 환경을 생성합니다. 여기서는 OpenAI Gym 라이브러리를 사용하여 FrozenLake 환경을 생성합니다.

```python
import gym
import numpy as np
import random

# FrozenLake-v1 환경 생성 (미끄러운 환경 비활성화)
env = gym.make('FrozenLake-v1', is_slippery=False)
# 환경 초기화
state = env.reset()
# 환경 정보 확인
print("상태 공간 크기:", env.observation_space) # 16 (4x4 격자)
print("행동 공간 크기:", env.action_space) # 4 (좌, 하, 우, 상)
```
<br>

2. 행동 선택 (Action Selection)<br>
에이전트는 현재 상태에 따라 행동을 선택합니다. 초기에는 무작위 행동을 선택할 수 있습니다. ε-greedy 전략을 사용하여 탐험(exploration)과 활용(exploitation)의 균형을 맞출 수 있습니다.

```python
# ε-greedy 전략에 따른 행동 선택
epsilon = 0.1 # 탐험 확률
if random.uniform(0, 1) < epsilon:
    action = env.action_space.sample() # 탐험: 무작위 행동 선택
else:
    action = np.argmax(q_table[state, :]) # 활용: 현재 Q-테이블에서 가장 높은 가치를 가진 행동 선택
print("선택된 행동:", action)
```
<br>

3. 환경과 상호작용 (Interaction with Environment)<br>
선택한 행동을 환경에 적용하고, 다음 상태, 보상, 종료 여부 등을 얻습니다.
```python
# 행동 수행
next_state, reward, done, info = env.step(action)
print("다음 상태:", next_state)
print("보상:", reward)
print("게임 종료 여부:", done)
print("추가 정보:", info)
# 환경 렌더링 (선택적, 텍스트 기반으로 환경을 보여줍니다)
env.render()
```
<br>

4. 보상 및 상태 전이 저장 (Storing Experience)<br>
에이전트는 경험(상태, 행동, 보상, 다음 상태)을 저장합니다. 이 경험은 학습에 사용됩니다.
```python
# 경험 저장 (간단한 예시로 리스트에 저장)
experience = (state, action, reward, next_state, done)
print("경험:", experience)
```
<br>

5. 학습 (Learning)<br>
저장된 경험을 이용하여 정책 또는 가치 함수를 업데이트합니다. 여기서는 가장 간단한 방법 중 하나인 *Q-러닝(Q-Learning)* 의 업데이트 규칙을 간략하게 보여드리겠습니다.

```python
# Q-테이블 초기화 (상태 x 행동 크기의 테이블)
q_table = np.zeros([env.observation_space.n, env.action_space.n])

# 학습 파라미터
learning_rate = 0.1
discount_factor = 0.9
epsilon = 0.1 # 탐험 확률

# Q-러닝 업데이트 규칙
if not done: # 게임이 끝나지 않았을 경우에만 업데이트
    best_next_q = np.max(q_table[next_state]) # 다음 상태에서 가장 높은 Q 값
    q_table[state, action] += learning_rate * (reward + discount_factor * best_next_q - q_table[state, action])

print("업데이트된 Q-테이블:\n", q_table)
```
<br>

6. 반복 (Iteration) <br>
위의 2~5단계를 반복하여 에이전트를 학습시킵니다.

<br><br>

### 강화학습(Reinforcement Learning)의 활용 분야
---
* 게임 AI: 게임 캐릭터의 행동 제어
* 로봇 공학: 로봇의 제어 및 작업 수행
* 자율 주행: 자동차의 주행 제어
* 추천 시스템: 사용자에게 상품 또는 콘텐츠 추천
* 금융: 주식 거래, 포트폴리오 관리

<br><br> 

## 예시
---
아래 코드는 OpenAI Gym 라이브러리의 FrozenLake 환경에서 Q-러닝의 기본적인 개념을 보여주는 간단한 예시입니다.
<br>

```python
import gym
import numpy as np
import random

# FrozenLake 환경 생성
env = gym.make('FrozenLake-v1', is_slippery=False) # 미끄러운 환경 비활성화

# Q-테이블 초기화 (상태 x 행동)
q_table = np.zeros([env.observation_space.n, env.action_space.n])

# 학습 파라미터
learning_rate = 0.1
discount_factor = 0.99
num_episodes = 1000

# Q-러닝 알고리즘
for i in range(num_episodes):
    state = env.reset()
    done = False
    while not done:
        # ε-greedy 전략 (탐험과 활용 균형)
        if random.uniform(0, 1) < 0.1: # 10% 확률로 탐험
            action = env.action_space.sample()
        else: # 90% 확률로 활용
            action = np.argmax(q_table[state, :])

        next_state, reward, done, _ = env.step(action)

        # Q-테이블 업데이트
        q_table[state, action] = q_table[state, action] + learning_rate * (reward + discount_factor * np.max(q_table[next_state, :]) - q_table[state, action])

        state = next_state

print("학습된 Q-테이블:")
print(q_table)

# 학습된 Q-테이블을 사용하여 게임 플레이
state = env.reset()
for _ in range(10):
    action = np.argmax(q_table[state, :])
    next_state, _, done, _ = env.step(action)
    env.render()
    state = next_state
    if done:
        break
env.close()
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}