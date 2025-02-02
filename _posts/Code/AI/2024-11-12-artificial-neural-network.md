---
title:  "[AI] 인공신경망(Artificial Neural Network)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Artificial Neural Network

categories:
  - AI
tags:
  - [AI, 인공신경망, Artificial Neural Network, ANN]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 인공신경망(Artificial Neural Network)의 개념
---
머신러닝의 핵심적인 개념 중 하나인 인공신경망(Artificial Neural Network, ANN)은 인간의 뇌의 신경망 구조를 모방하여 만든 계산 모델입니다. <br> 마치 우리 뇌의 뉴런들이 서로 연결되어 정보를 처리하는 방식처럼, 인공신경망은 여러 개의 노드(node) 또는 *뉴런(neuron)* 들이 연결되어 네트워크를 형성하고, 이 네트워크를 통해 정보를 처리하고 학습합니다.

좀 더 구체적으로 설명하자면, 인공신경망은 입력층(input layer), 은닉층(hidden layer) (선택적), 그리고 *출력층(output layer)* 으로 구성됩니다. 입력층은 외부에서 데이터를 받아들이는 역할을 하고, 은닉층은 입력 데이터를 변환하고 추상화하는 역할을 하며, 출력층은 최종 결과를 출력하는 역할을 합니다. 각 노드는 이전 층의 노드들로부터 입력을 받아 가중치(weight)를 곱하고, 활성화 함수(activation function)를 거쳐 다음 층으로 출력을 전달합니다. <br>이러한 과정을 통해 네트워크는 입력 데이터에서 패턴을 학습하고, 예측이나 분류 등의 작업을 수행할 수 있게 됩니다.
<br>

![Image](https://github.com/user-attachments/assets/8a6b2685-7bd6-4ad1-932a-f57c9bb23222)
(출처 : https://www.geeksforgeeks.org/artificial-neural-networks-and-its-applications/)<br><br>


### 인공신경망(Artificial Neural Network)의 기본 구조
---
인공신경망은 크게 세 가지 층으로 구성됩니다.

* 입력층(Input Layer): 외부에서 데이터를 입력받는 층입니다. 입력 데이터의 각 특징(feature)에 해당하는 뉴런으로 구성됩니다. 예를 들어, 이미지 인식 문제에서 각 픽셀의 색상 값이 입력층의 뉴런에 해당될 수 있습니다.

* 은닉층(Hidden Layer): 입력층과 출력층 사이에 위치하며, 입력 데이터를 변환하고 추상화하는 역할을 합니다. 은닉층은 여러 개가 존재할 수 있으며, 각 은닉층은 이전 층의 출력을 입력으로 받아 처리합니다. 은닉층의 뉴런 개수는 문제의 복잡성에 따라 조절됩니다.

* 출력층(Output Layer): 최종 결과를 출력하는 층입니다. 문제의 종류에 따라 다양한 형태를 가질 수 있습니다. 예를 들어, 분류 문제에서는 각 클래스에 대한 확률 값을 출력하는 형태를 가질 수 있고, 회귀 문제에서는 연속적인 값을 출력하는 형태를 가질 수 있습니다.
<br><br>

#### 뉴런 (Neuron)
---
뉴런은 인공신경망의 기본 단위로, 입력 신호를 받아 처리하고 출력 신호를 생성하는 역할을 합니다. 각 뉴런은 다음과 같은 요소들로 구성됩니다.

* 입력 (Input): 이전 층의 뉴런으로부터 전달된 신호입니다.
* 가중치 (Weight): 각 입력 신호의 중요도를 나타내는 값입니다.
* 편향 (Bias): 뉴런의 활성화 여부를 조절하는 값입니다.
* 활성화 함수 (Activation Function): 뉴런의 출력을 결정하는 함수입니다. 입력 신호와 가중치를 곱하고 편향을 더한 값을 활성화 함수에 적용하여 출력 신호를 생성합니다.
<br><br>

#### 연결 (Connection)
---
뉴런과 뉴런 사이의 연결은 가중치를 통해 표현됩니다. 가중치는 입력 신호가 다음 뉴런에 얼마나 큰 영향을 미치는지 나타냅니다. 가중치가 클수록 해당 입력 신호는 다음 뉴런에 더 큰 영향을 미칩니다.
<br><br>

#### 활성화 함수 (Activation Function)
---
활성화 함수는 뉴런의 출력을 결정하는 중요한 역할을 합니다. 활성화 함수는 선형 변환된 입력 신호에 비선형성을 추가하여 신경망이 복잡한 패턴을 학습할 수 있도록 합니다. 대표적인 활성화 함수는 다음과 같습니다.

* 시그모이드 함수 (Sigmoid Function): 0과 1 사이의 값을 출력하는 함수로, 확률 값을 표현하는 데 사용됩니다.
* ReLU 함수 (Rectified Linear Unit Function): 입력값이 0보다 작으면 0을 출력하고, 0보다 크면 입력값을 그대로 출력하는 함수입니다.
* tanh 함수 (Hyperbolic Tangent Function): -1과 1 사이의 값을 출력하는 함수입니다.
<br><br>


### 인공신경망(Artificial Neural Network)의 종류
---
* 다층 퍼셉트론 (Multilayer Perceptron, MLP): 여러 개의 은닉층을 가진 기본적인 형태의 신경망입니다.
* 합성곱 신경망 (Convolutional Neural Network, CNN): 이미지 처리에 특화된 신경망으로, 합성곱 연산을 사용하여 이미지의 특징을 추출합니다.
* 순환 신경망 (Recurrent Neural Network, RNN): 시퀀스 데이터 처리에 특화된 신경망으로, 이전 시점의 정보를 기억하는 메커니즘을 가지고 있습니다.
* 심층 신경망 (Deep Neural Network, DNN): 여러 개의 은닉층을 가진 신경망을 통칭하는 용어입니다.
<br><br>

### 인공신경망(Artificial Neural Network)의 활용 분야
---
* 이미지 인식: 사진 속 객체 인식, 얼굴 인식, 이미지 분류
* 자연어 처리: 텍스트 분류, 기계 번역, 챗봇, 감성 분석
* 음성 인식: 음성 명령 인식, 음성-텍스트 변환
* 추천 시스템: 사용자 맞춤형 상품 추천, 콘텐츠 추천
* 의료: 질병 진단, 의료 영상 분석, 신약 개발
* 금융: 주가 예측, 신용 평가, 사기 탐지
<br><br>

### 인공신경망(Artificial Neural Network)의 과정
---

1. 데이터 준비 : 인공신경망 학습에 사용할 데이터를 준비합니다. 입력 데이터와 정답(label) 데이터로 구성됩니다.
```python
import numpy as np

# 입력 데이터 (2개의 특징을 가진 4개의 데이터 샘플)
X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])

# 정답 데이터 (각 입력 데이터에 대한 정답)
y = np.array([0, 1, 1, 0])
```
<br>

2. 모델 정의 (Model Definition) : 인공신경망의 구조를 정의합니다. 여기서는 2개의 입력 뉴런, 2개의 은닉층 뉴런, 1개의 출력 뉴런을 가진 간단한 신경망을 사용하겠습니다.
```python
def sigmoid(x):
    """시그모이드 활성화 함수"""
    return 1 / (1 + np.exp(-x))

def sigmoid_derivative(x):
    """시그모이드 함수의 도함수"""
    return x * (1 - x)

# 가중치와 편향 초기화 (랜덤 값으로 초기화)
input_neurons = 2
hidden_neurons = 2
output_neurons = 1

weights_input_hidden = np.random.uniform(size=(input_neurons, hidden_neurons))
bias_hidden = np.random.uniform(size=(hidden_neurons,))
weights_hidden_output = np.random.uniform(size=(hidden_neurons, output_neurons))
bias_output = np.random.uniform(size=(output_neurons,))
```
<br>

3. 순전파 (Forward Propagation): 입력층에서 시작하여 은닉층, 출력층 순으로 신호를 전달합니다. 각 뉴런에서 입력 신호와 가중치를 곱하고 편향을 더한 후 활성화 함수를 적용하여 출력 신호를 생성합니다.
```python
def forward_propagation(X):
    """순전파 함수"""
    hidden_input = np.dot(X, weights_input_hidden) + bias_hidden
    hidden_output = sigmoid(hidden_input)

    output_input = np.dot(hidden_output, weights_hidden_output) + bias_output
    output = sigmoid(output_input)

    return hidden_output, output

hidden_output, output = forward_propagation(X)

print("순전파 결과:")
print("은닉층 출력:\n", hidden_output)
print("출력층 출력:\n", output)
```
<br>

4. 역전파 (Backpropagation): 출력층에서 계산된 오차를 바탕으로 가중치와 편향을 업데이트합니다. 경사 하강법(Gradient Descent) 알고리즘을 사용하여 오차를 최소화하는 방향으로 가중치를 조절합니다.<br>

```python
def backpropagation(X, hidden_output, output, y):
    """역전파 함수"""
    output_delta = (y - output) * sigmoid_derivative(output)
    d_weights_hidden_output = np.dot(hidden_output.T, output_delta)
    d_bias_output = np.sum(output_delta, axis=0, keepdims=True)

    hidden_delta = output_delta.dot(weights_hidden_output.T) * sigmoid_derivative(hidden_output)
    d_weights_input_hidden = np.dot(X.T, hidden_delta)
    d_bias_hidden = np.sum(hidden_delta, axis=0, keepdims=True)

    return d_weights_input_hidden, d_bias_hidden, d_weights_hidden_output, d_bias_output

d_weights_input_hidden, d_bias_hidden, d_weights_hidden_output, d_bias_output = backpropagation(X, hidden_output, output, y)

print("역전파 결과:")
print("입력층-은닉층 가중치 변화량:\n", d_weights_input_hidden)
print("은닉층 편향 변화량:\n", d_bias_hidden)
print("은닉층-출력층 가중치 변화량:\n", d_weights_hidden_output)
print("출력층 편향 변화량:\n", d_bias_output)
```
<br>

5. 학습 (Training): 순전파와 역전파 과정을 반복하면서 가중치와 편향을 최적화합니다. 학습 데이터를 이용하여 신경망의 성능을 향상시키는 과정입니다.

```python
epochs = 10000
learning_rate = 0.1

for epoch in range(epochs):
    hidden_output, output = forward_propagation(X)
    loss = calculate_loss(y, output)

    d_weights_input_hidden, d_bias_hidden, d_weights_hidden_output, d_bias_output = backpropagation(X, hidden_output, output, y)

    weights_input_hidden += learning_rate * d_weights_input_hidden
    bias_hidden += learning_rate * d_bias_hidden
    weights_hidden_output += learning_rate * d_weights_hidden_output
    bias_output += learning_rate * d_bias_output

    if epoch % 1000 == 0:
        print(f"Epoch: {epoch}, Loss: {loss}")

print("학습 후 가중치 및 편향:")
print("입력층-은닉층 가중치:\n", weights_input_hidden)
print("은닉층 편향:\n", bias_hidden)
print("은닉층-출력층 가중치:\n", weights_hidden_output)
print("출력층 편향:\n", bias_output)
```

<br><br>

[간략화된 역전파 포함 전체 코드]
```c#
import numpy as np
import matplotlib.pyplot as plt

# 입력 데이터
X = np.array([[0.5, 0.8], [0.2, 0.9], [0.7, 0.1], [0.1, 0.3]])
y = np.array([[1], [0], [1], [0]])
input_dim = X.shape[1]
output_dim = y.shape[1]

# 초기 가중치 및 편향
hidden_dim = 3
weights_input_hidden = np.random.randn(input_dim, hidden_dim)
bias_hidden = np.zeros((1, hidden_dim))
weights_hidden_output = np.random.randn(hidden_dim, output_dim)
bias_output = np.zeros((1, output_dim))

# 활성화 함수
def sigmoid(x):
    return 1 / (1 + np.exp(-x))

# 학습 파라미터
learning_rate = 0.1
epochs = 1000

# 학습 루프
for epoch in range(epochs):
    for i in range(len(X)):
        xi = X[i].reshape(1, -1)
        yi = y[i].reshape(1, -1)

        # 순전파
        hidden_input = np.dot(xi, weights_input_hidden) + bias_hidden
        hidden_output = sigmoid(hidden_input)
        output_input = np.dot(hidden_output, weights_hidden_output) + bias_output
        output = sigmoid(output_input)

        # 역전파 (간략화)
        output_error = output - yi
        weights_hidden_output -= learning_rate * np.dot(hidden_output.T, output_error)
        bias_output -= learning_rate * output_error

        hidden_error = np.dot(output_error, weights_hidden_output.T) * hidden_output * (1- hidden_output)
        weights_input_hidden -= learning_rate * np.dot(xi.T, hidden_error)
        bias_hidden -= learning_rate * hidden_error
        
print("학습 후 가중치 (입력->은닉):\n", weights_input_hidden)
print("학습 후 편향 (은닉):\n", bias_hidden)
print("학습 후 가중치 (은닉->출력):\n", weights_hidden_output)
print("학습 후 편향 (출력):\n", bias_output)
```

<br>


## 코드
---
Keras를 사용하여 간단한 분류 문제를 해결하는 인공신경망 예시 코드입니다.
<br>

```c#
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers

# 가상 데이터 생성
num_samples = 1000
X = np.random.rand(num_samples, 2) # 2개의 특징
y = (X[:, 0] + X[:, 1] > 1).astype(int) # 간단한 분류 규칙

# 모델 정의
model = keras.Sequential(
    [
        keras.Input(shape=(2,)), # 입력층
        layers.Dense(4, activation="relu"), # 은닉층 (4개의 뉴런)
        layers.Dense(1, activation="sigmoid"), # 출력층 (이진 분류이므로 시그모이드 활성화 함수 사용)
    ]
)

# 모델 컴파일
model.compile(loss="binary_crossentropy", optimizer="adam", metrics=["accuracy"])

# 모델 학습
model.fit(X, y, epochs=10, batch_size=32)

loss, accuracy = model.evaluate(X, y, verbose=0)
print(f"Loss: {loss:.4f}")
print(f"Accuracy: {accuracy:.4f}")
```


<br> 

[Top](#){: .btn .btn--primary }{: .align-right}