---
title: "[AI] 경사 하강법(Gradient Descent)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Gradient Descent

categories:
  - AI
tags:
  - [AI, 경사 하강법, Gradient Descent]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 경사 하강법(Gradient Descent)의 개념
---
경사 하강법은 함수의 최솟값을 찾기 위한 반복적인 최적화 알고리즘입니다. 마치 안개 낀 산에서 가장 낮은 곳으로 내려가는 것과 같습니다. 앞이 보이지 않기 때문에 주변의 경사를 확인하면서 가장 가파른 내리막길을 따라 한 걸음씩 내려가다 보면 결국에는 골짜기(최솟값)에 도달하게 됩니다.

머신러닝에서는 모델의 예측값과 실제값 사이의 오차를 나타내는 손실 함수(Loss Function) 또는 비용 함수(Cost Function)를 최소화하는 것이 목표입니다. 경사 하강법은 이 손실 함수의 최솟값을 찾기 위해 사용됩니다.
<br><br>

![Image](https://github.com/user-attachments/assets/1e2b3280-8e2a-4789-9588-7165ef9bbad8)
(출처 : https://www.linkedin.com/pulse/understanding-gradient-descent-algorithm-its-role-linear-mhango-kjbvf/)<br><br>


### 경사 (Gradient) 란?
---
경사는 다변수 함수에서 각 변수에 대한 편미분 벡터를 의미합니다. 즉, 각 방향으로의 기울기를 나타내는 벡터입니다. 2차원 공간에서 기울기는 단순히 함수의 접선의 기울기를 의미하지만, 다차원 공간에서는 각 차원 방향의 기울기를 모두 고려해야 합니다. 마치 여러 방향으로 기울어진 산에서 각 방향의 기울기를 모두 고려하여 내려갈 방향을 정하는 것과 같습니다.
<br><br>

### 학습률 (Learning Rate)
---
학학습률은 가중치를 얼마나 크게 업데이트할지를 결정하는 중요한 하이퍼파라미터입니다. 마치 산에서 한 걸음씩 내려갈 때, 한 걸음의 크기를 결정하는 것과 같습니다.

* 학습률이 너무 큰 경우: 최솟값을 지나쳐 발산할 수 있습니다. 마치 너무 성큼성큼 내려가다가 골짜기를 지나쳐 반대편으로 올라가는 것과 같습니다.
* 학습률이 너무 작은 경우: 최솟값에 도달하는 데 너무 오랜 시간이 걸릴 수 있습니다. 마치 너무 조금씩 내려가서 목적지에 늦게 도착하는 것과 같습니다.

적절한 학습률을 찾는 것은 중요하며, 다양한 방법을 통해 최적의 값을 찾을 수 있습니다 (예: learning rate scheduling).
<br><br> 

### 경사 하강법의 작동 원리
---
경사 하강법은 다음과 같은 단계를 반복합니다.

1. 초기 가중치(Weight) 설정: 모델의 가중치를 임의의 값으로 초기화합니다.
2. 경사 계산: 현재 가중치에서 손실 함수의 경사를 계산합니다.
3. 가중치 업데이트: 계산된 경사의 반대 방향으로 가중치를 업데이트합니다. 이때, *학습률(Learning Rate)*이라는 값을 곱하여 얼마나 크게 이동할지 조절합니다.
4. 2~3단계를 반복합니다.

가중치 업데이트는 다음과 같은 식으로 표현됩니다.

```
w_new = w_old - learning_rate * gradient
```
```w_new```: 새로운 가중치
```w_old```: 이전 가중치
```learning_rate```: 학습률 (보통 0.001, 0.01, 0.1 등의 작은 값을 사용)
```gradient```: 손실 함수의 경사

<br>

### 경사 하강법(Gradient Descent)의 종류
---

공통적으로 아래의 데이터 생성을 한 이후 각각의 경사하강법을 사용하는 흐름입니다.

```python
import numpy as np
import matplotlib.pyplot as plt

# 가상 데이터 생성
np.random.seed(0)
X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)

# X에 bias term 추가 (편향 b 계산을 용이하게 하기 위함)
X_b = np.c_[np.ones((100, 1)), X] # 모든 입력 x에 x0 = 1을 추가합니다.
```
<br>

* 배치 경사 하강법 (Batch Gradient Descent) <br>
모든 학습 데이터를 사용하여 경사를 계산합니다. 계산량이 많지만, 안정적인 수렴을 보입니다. 마치 산 전체의 경사를 한 번에 파악하여 내려갈 방향을 정하는 것과 같습니다.<br><br>

```python
# 초기 가중치 설정
theta = np.random.randn(2, 1)  # bias term 때문에 2개의 가중치 필요

# 학습률 및 반복 횟수 설정
learning_rate = 0.1
n_iterations = 1000

# 배치 경사 하강법
for iteration in range(n_iterations):
    gradients = 2 / len(X) * X_b.T.dot(X_b.dot(theta) - y)
    theta = theta - learning_rate * gradients

# 결과 출력
print("배치 경사 하강법 결과:")
print(f"가중치 (theta): {theta}") # 출력 예시: [[3.90306161] [2.97237142]]

# 시각화
plt.scatter(X, y)
X_new = np.array([[0], [2]])
X_new_b = np.c_[np.ones((2, 1)), X_new]
y_predict = X_new_b.dot(theta)
plt.plot(X_new, y_predict, "r-")
plt.xlabel("X")
plt.ylabel("y")
plt.title("Batch Gradient Descent")
plt.show()
```
<br>

* 확률적 경사 하강법 (Stochastic Gradient Descent, SGD) <br>
학습 데이터 중 하나의 데이터만 사용하여 경사를 계산합니다. 계산 속도가 빠르지만, 불안정한 수렴을 보일 수 있습니다. 마치 산의 일부분의 경사만 보고 내려갈 방향을 정하는 것과 같아서, 방향이 자주 바뀔 수 있습니다. 학습률 스케줄링을 통해 이러한 불안정성을 완화할 수 있습니다.<br><br>

```python
# 초기 가중치 설정
theta = np.random.randn(2, 1)

# 학습 파라미터
n_epochs = 50
t0, t1 = 5, 50  # 학습 스케줄 하이퍼파라미터

def learning_schedule(t):
    return t0 / (t + t1)

# 확률적 경사 하강법
for epoch in range(n_epochs):
    for i in range(len(X)):
        random_index = np.random.randint(len(X))
        xi = X_b[random_index:random_index + 1]
        yi = y[random_index:random_index + 1]
        gradients = 2 * xi.T.dot(xi.dot(theta) - yi)
        learning_rate = learning_schedule(epoch * len(X) + i) # 학습 스케줄링 적용
        theta = theta - learning_rate * gradients

# 결과 출력
print("\n확률적 경사 하강법 결과:")
print(f"가중치 (theta): {theta}") # 출력 예시: [[3.98777977] [2.98663854]]

# 시각화
plt.scatter(X, y)
X_new = np.array([[0], [2]])
```
<br>

* 미니 배치 경사 하강법 (Mini-Batch Gradient Descent) <br>
학습 데이터를 작은 배치로 나누어 각 배치에 대해 경사를 계산합니다. 배치 경사 하강법과 확률적 경사 하강법의 중간 형태이며, 대부분의 경우 효과적인 방법입니다. 마치 산의 여러 지점을 동시에 탐색하여 내려갈 방향을 정하는 것과 같습니다.<br><br>

```python
# 초기 가중치 설정
theta = np.random.randn(2, 1)

# 학습 파라미터
n_epochs = 50
minibatch_size = 20
learning_rate = 0.01

# 미니 배치 경사 하강법
for epoch in range(n_epochs):
    shuffled_indices = np.random.permutation(len(X)) # 각 epoch마다 데이터 셔플링
    X_b_shuffled = X_b[shuffled_indices]
    y_shuffled = y[shuffled_indices]
    for i in range(0, len(X), minibatch_size):
        xi = X_b_shuffled[i:i + minibatch_size]
        yi = y_shuffled[i:i + minibatch_size]
        gradients = 2 / len(xi) * xi.T.dot(xi.dot(theta) - yi)
        theta = theta - learning_rate * gradients

# 결과 출력
print("\n미니 배치 경사 하강법 결과:")
print(f"가중치 (theta): {theta}") # 출력 예시: [[3.96140139] [2.99020959]]

# 시각화
plt.scatter(X, y)
X_new = np.array([[0], [2]])
X_new_b = np.c_[np.ones((2, 1)), X_new]
y_predict = X_new_b.dot(theta)
plt.plot(X_new, y_predict, "r-")
plt.xlabel("X")
plt.ylabel("y")
plt.title("Mini-Batch Gradient Descent")
plt.show()
```
<br>

## 예시
---
Python으로 간단한 선형 회귀 문제를 경사 하강법으로 푸는 예시 코드입니다.
<br>

```python
import numpy as np
import matplotlib.pyplot as plt

# 가상 데이터 생성 (위와 동일)
np.random.seed(0)
X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)
X_b = np.c_[np.ones((100, 1)), X]

# 초기 가중치 설정
theta = np.random.randn(2, 1) # bias term을 포함하므로 2개

# 학습률 및 반복 횟수 설정
learning_rate = 0.01
n_iterations = 1000

# 경사 하강법
for _ in range(n_iterations):
    y_pred = X_b.dot(theta) # 예측값 계산 (bias term 포함)
    error = y_pred - y
    gradients = 2 / len(X) * X_b.T.dot(error)
    theta = theta - learning_rate * gradients

# 결과 출력
print("\n기존 방식 경사 하강법 결과:")
print(f"가중치 (theta): {theta}") # 출력 예시: [[3.90306161] [2.97237142]]

# 시각화 (위와 동일)
plt.scatter(X, y)
X_new = np.array([[0], [2]])
X_new_b = np.c_[np.ones((2, 1)), X_new]
y_predict = X_new_b.dot(theta)
plt.plot(X_new, y_predict, "r-")
plt.xlabel("X")
plt.ylabel("y")
plt.title("Original Gradient Descent")
plt.show()
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}