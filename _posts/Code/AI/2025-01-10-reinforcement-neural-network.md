---
title:  "[AI] 강화 학습 신경망(Reinforcement Neural Network)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Reinforcement Neural Network

categories:
  - AI
tags:
  - [AI, 강화 학습 신경망, Reinforcement Neural Network, RNN]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 강화 학습 신경망(Reinforcement Neural Network)의 개념
---
강화 학습 신경망(Reinforcement Neural Network, RNN)은 **강화 학습(Reinforcement Learning)**과 **심층 신경망(Deep Neural Network)**을 결합한 형태입니다. 강화 학습은 **에이전트(Agent)**가 **환경(Environment)**과 상호작용하며 **보상(Reward)**을 최대화하는 방향으로 학습하는 방식입니다. 마치 **"당근과 채찍"**을 통해 동물을 훈련시키는 것과 유사합니다. <br>
RNN은 이러한 강화 학습 과정을 심층 신경망을 통해 더욱 효과적으로 수행합니다.
<br><br>

![Image](https://github.com/user-attachments/assets/58feb68d-1141-4548-a9af-e02a8e51ff72)<br>
(출처 : https://www.researchgate.net/figure/Deep-reinforcement-learning-scheme-A-deep-neural-network-learns-the-policy_fig1_360910430)<br><br>


### 강화 학습 신경망(Reinforcement Neural Network)의 특징
---
* End-to-End 학습: 입력부터 출력까지 전체 과정을 신경망을 통해 직접 학습합니다.
* 높은 표현력: 심층 신경망을 사용하여 복잡한 함수 관계를 표현할 수 있습니다.
* 다양한 알고리즘 적용: Q-Learning, Policy Gradient 등 다양한 강화 학습 알고리즘을 적용할 수 있습니다.
* 현실 세계 문제 해결: 게임, 로봇 제어, 자연어 처리 등 다양한 현실 세계 문제 해결에 적용 가능합니다.
<br><br>

### 강화 학습 신경망(Reinforcement Neural Network)의 종류
---
* Q-Learning: Q-value를 사용하여 최적의 행동을 학습하는 방법입니다.
* Deep Q-Network (DQN): Q-Learning에 심층 신경망을 적용한 방법입니다.
* Policy Gradient: 정책 함수를 직접 학습하여 최적의 행동을 선택하는 방법입니다.
* Actor-Critic: Actor와 Critic 두 개의 신경망을 사용하여 학습하는 방법입니다.
<br><br>

### 강화 학습 신경망(Reinforcement Neural Network)의 장단점
---
#### 장점
* 높은 성능: 복잡한 문제를 해결하는 데 뛰어난 성능을 보입니다.
* 자율 학습: 스스로 학습하므로, 사람이 직접 설계하기 어려운 전략을 학습할 수 있습니다.
* 다양한 분야 적용: 게임, 로봇 제어, 자연어 처리 등 다양한 분야에 적용 가능합니다.

#### 단점
* 학습 어려움: 학습이 불안정하거나 수렴하지 않을 수 있습니다.
* 많은 데이터 필요: 학습에 많은 데이터가 필요합니다.
* 계산 비용: 학습에 많은 계산 비용이 소요될 수 있습니다.
<br><br>

### 강화 학습 신경망(Reinforcement Neural Network)의 과정
---
1. 상태 관찰(Observation): 에이전트는 현재 환경 상태를 관찰합니다. 관찰 결과는 신경망의 입력으로 사용됩니다.
2. 행동 선택(Action Selection): 신경망은 관찰 결과를 바탕으로 최적의 행동을 선택합니다.
3. 행동 수행(Action Execution): 에이전트는 선택된 행동을 실제로 수행합니다.
4. 보상 획득(Reward Acquisition): 에이전트는 행동에 대한 보상 또는 벌칙을 받습니다.
5. 학습(Learning): 에이전트는 받은 보상을 바탕으로 신경망의 가중치를 업데이트하여 행동 전략을 개선합니다.
6. 반복(Iteration): 위 과정을 반복하며 학습을 진행합니다.
<br><br>

[PyTorch 활용, 각과정 샘플 코드]
```python
import torch
import torch.nn as nn
import torch.optim as optim
import gym

# 신경망 모델 정의
class QNetwork(nn.Module):
    def __init__(self, input_dim, output_dim):
        super(QNetwork, self).__init__()
        self.fc = nn.Sequential(
            nn.Linear(input_dim, 128),
            nn.ReLU(),
            nn.Linear(128, 128),
            nn.ReLU(),
            nn.Linear(128, output_dim)
        )

    def forward(self, x):
        return self.fc(x)

# 환경 생성
env = gym.make('CartPole-v1')

# 모델 생성
input_dim = env.observation_space.shape[0]
output_dim = env.action_space.n
model = QNetwork(input_dim, output_dim)

# 손실 함수 및 최적화 함수 정의
criterion = nn.MSELoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 학습
num_episodes = 1000
for episode in range(num_episodes):
    state = env.reset()
    done = False
    while not done:
        # 행동 선택
        state = torch.FloatTensor(state).unsqueeze(0)
        q_values = model(state)
        action = torch.argmax(q_values).item()

        # 행동 수행 및 보상 획득
        next_state, reward, done, _ = env.step(action)

        # 학습
        next_state = torch.FloatTensor(next_state).unsqueeze(0)
        target_q_values = model(next_state).detach()
        target_q_values[0][action] = reward + (1 - done) * 0.99 * torch.max(target_q_values)
        loss = criterion(q_values, target_q_values)

        optimizer.zero_grad()
        loss.backward()
        optimizer.step()

        state = next_state

    if episode % 100 == 0:
        print(f"Episode: {episode}, Loss: {loss.item()}")

env.close()
```
<br><br>

### 강화 학습 신경망(Reinforcement Neural Network) 사용 시 주의사항
---
* 환경 설정: 학습에 적합한 환경을 설정하는 것이 중요합니다.
* 보상 함수 설계: 적절한 보상 함수를 설계해야 합니다.
* 하이퍼파라미터 튜닝: 학습 효율을 높이기 위해 하이퍼파라미터를 적절하게 튜닝해야 합니다.
* 안정적인 학습: 학습이 불안정하거나 발산하지 않도록 학습 과정을 안정화해야 합니다.
<br><br> 

## 예시
---
[Python, Stable Baselines3 활용, DQN 알고리즘]
```python
import gym
from stable_baselines3 import DQN

env = gym.make('CartPole-v1')

model = DQN('MlpPolicy', env, verbose=1)
model.learn(total_timesteps=10000)

obs = env.reset()
for i in range(1000):
    action, _states = model.predict(obs)
    obs, rewards, dones, info = env.step(action)
    env.render()
    if dones:
        print("Episode finished after {} timesteps".format(i+1))
        obs = env.reset()
env.close()
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}