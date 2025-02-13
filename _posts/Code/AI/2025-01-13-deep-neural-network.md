---
title:  "[AI] 심층 신경망(Deep Neural Network)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Deep Neural Network

categories:
  - AI
tags:
  - [AI, 인공신경망, Deep Neural Network, DNN]

toc: true
toc_sticky: true
 
date: 2025-01-13
last_modified_at: 2025-01-13
---

## 심층 신경망(Deep Neural Network)의 개념
---
심층 신경망(Deep Neural Network, DNN)은 **인공 신경망(Artificial Neural Network)**의 한 종류로, **여러 개의 은닉층(Hidden Layer)**을 가진 신경망을 의미합니다. 마치 **"뇌의 구조"**를 모방한 DNN은 복잡한 패턴을 학습하고 높은 수준의 추론 능력을 보여줍니다. 이미지 인식, 자연어 처리, 음성 인식 등 다양한 분야에서 핵심적인 역할을 수행합니다.
<br><br>

![Image](https://github.com/user-attachments/assets/9f4845ec-2fcb-4608-a898-9b4885e7d261)<br>
(출처 : https://www.researchgate.net/figure/Deep-Neural-Network-DNN-example_fig2_341037496)<br><br>


### 심층 신경망(Deep Neural Network)의 특징
---
높은 표현력(High Representation Power): 여러 개의 은닉층을 통해 복잡한 비선형 관계를 학습하고 표현할 수 있습니다.
Feature Extraction: 입력 데이터에서 유용한 특징을 자동으로 추출하여 학습에 활용합니다.
End-to-End 학습: 입력부터 출력까지 전체 과정을 신경망을 통해 직접 학습합니다.
다양한 구조: 다양한 구조(Fully Connected, Convolutional, Recurrent 등)를 통해 다양한 종류의 데이터를 처리할 수 있습니다.
<br><br>

### 심층 신경망(Deep Neural Network)의 종류
---
* Fully Connected Network (FCN): 모든 노드가 서로 연결된 기본적인 형태의 신경망입니다.
* Convolutional Neural Network (CNN): 이미지 데이터 처리에 특화된 신경망입니다. Convolution 연산과 Pooling 연산을 사용하여 이미지의 특징을 추출합니다.
* Recurrent Neural Network (RNN): 순차적인 데이터(텍스트, 음성 등) 처리에 특화된 신경망입니다. 이전 시점의 정보를 활용하여 현재 시점의 데이터를 처리합니다.
<br><br>

### 장단점
---
#### 장점
* 높은 성능: 복잡한 패턴을 학습하고 높은 수준의 추론 능력을 보여줍니다.
* Feature Extraction: 입력 데이터에서 유용한 특징을 자동으로 추출하여 학습에 활용합니다.
* 다양한 분야 적용: 이미지 인식, 자연어 처리, 음성 인식 등 다양한 분야에 적용 가능합니다.
#### 단점
* 학습 데이터: 학습에 많은 양의 데이터가 필요합니다.
* 계산 비용: 학습에 많은 계산 비용이 소요될 수 있습니다.
* Overfitting: 과적합(Overfitting)이 발생할 수 있습니다.
* Hyperparameter Tuning: 적절한 하이퍼파라미터를 찾는 것이 중요합니다.
<br><br>

### 심층 신경망(Deep Neural Network)의 과정
---
1. 입력(Input): 입력 데이터는 입력층(Input Layer)을 통해 신경망에 전달됩니다.
2. 가중치(Weight): 각 연결은 가중치를 가지며, 가중치는 입력 신호의 강도를 조절합니다.
3. 활성화 함수(Activation Function): 각 노드는 활성화 함수를 통해 입력 신호를 변환합니다. 활성화 함수는 비선형성을 추가하여 신경망의 표현력을 높입니다.
4. 은닉층(Hidden Layer): 은닉층은 입력 신호를 처리하고 특징을 추출하는 역할을 합니다. 여러 개의 은닉층을 거치면서 데이터는 점차 추상화되고 고차원적인 특징으로 변환됩니다.
5. 출력층(Output Layer): 출력층은 최종 결과를 출력합니다. 출력층의 노드 개수와 활성화 함수는 문제의 종류에 따라 달라집니다.
6. 손실 함수(Loss Function): 실제 출력과 정답을 비교하여 손실 값을 계산합니다. 손실 값은 신경망의 성능을 평가하는 지표로 사용됩니다.
7. 역전파(Backpropagation): 손실 값을 바탕으로 가중치를 업데이트하여 신경망의 성능을 개선합니다.
8. 반복(Iteration): 위 과정을 반복하며 학습을 진행합니다.
<br><br>

[Python, TensorFlow/Keras 활용]
```python
import tensorflow as tf

# 모델 정의
model = tf.keras.models.Sequential([
    tf.keras.layers.Dense(128, activation='relu', input_shape=(784,)), # 입력층
    tf.keras.layers.Dense(10, activation='softmax') # 출력층
])

# 모델 컴파일
model.compile(optimizer='adam',
              loss='categorical_crossentropy',
              metrics=['accuracy'])

# 데이터 준비
(x_train, y_train), (x_test, y_test) = tf.keras.datasets.mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0 # 데이터 정규화
y_train = tf.keras.utils.to_categorical(y_train, num_classes=10) # One-hot encoding
y_test = tf.keras.utils.to_categorical(y_test, num_classes=10) # One-hot encoding

# 학습
model.fit(x_train, y_train, epochs=5)

# 평가
loss, accuracy = model.evaluate(x_test, y_test, verbose=0)
print('Test Loss:', loss)
print('Test Accuracy:', accuracy)
```
<br><br>

### 심층 신경망(Deep Neural Network)사용 시 주의사항
---
* 데이터 전처리: 학습 데이터를 적절하게 전처리하는 것이 중요합니다. 결측값 처리, 이상치 제거, 데이터 정규화 등을 고려해야 합니다.
* Overfitting 방지: 과적합을 방지하기 위해 Dropout, Regularization, Early Stopping 등의 기법을 사용해야 합니다.
* Hyperparameter Tuning: 적절한 하이퍼파라미터(학습률, 배치 크기, 은닉층 개수, 노드 개수 등)를 찾는 것이 중요합니다. Grid Search, Random Search, Bayesian Optimization 등의 방법을 사용할 수 있습니다.
<br><br> 

## 예시
---
[사과와 복숭아를 구분해보자! (Python, TensorFlow/Keras 활용)]
```python
import tensorflow as tf
import numpy as np
from sklearn.model_selection import train_test_split

# 1. 데이터 준비

# 샘플 데이터 (사과: 0, 복숭아: 1)
# 실제 데이터는 이미지 형태로 제공되어야 하며,
# 각 이미지는 1차원 배열로 펼쳐져야 합니다.
# 여기서는 간단한 설명을 위해 임의의 값을 사용합니다.
apple_data = np.random.rand(100, 784)  # 100개의 사과 데이터, 각 데이터는 784개의 특징
peach_data = np.random.rand(100, 784)  # 100개의 복숭아 데이터, 각 데이터는 784개의 특징

# 레이블 생성
apple_labels = np.zeros(100)  # 사과: 0
peach_labels = np.ones(100)  # 복숭아: 1

# 데이터 병합 및 섞기
data = np.concatenate((apple_data, peach_data))
labels = np.concatenate((apple_labels, peach_labels))

# 데이터를 훈련 데이터와 테스트 데이터로 분할
x_train, x_test, y_train, y_test = train_test_split(data, labels, test_size=0.2, random_state=42)

# 2. 모델 정의

model = tf.keras.models.Sequential([
    tf.keras.layers.Dense(128, activation='relu', input_shape=(784,)),  # 입력층 (784개의 특징)
    tf.keras.layers.Dense(64, activation='relu'),  # 은닉층 1
    tf.keras.layers.Dense(32, activation='relu'),  # 은닉층 2
    tf.keras.layers.Dense(1, activation='sigmoid')  # 출력층 (0 또는 1)
])

# 3. 모델 컴파일

model.compile(optimizer='adam',
              loss='binary_crossentropy',  # 이진 분류 문제
              metrics=['accuracy'])

# 4. 모델 학습

model.fit(x_train, y_train, epochs=10, batch_size=32)

# 5. 모델 평가

loss, accuracy = model.evaluate(x_test, y_test, verbose=0)
print('Test Loss:', loss)
print('Test Accuracy:', accuracy)

# 6. 예측

# 새로운 데이터로 예측
new_data = np.random.rand(10, 784)  # 10개의 새로운 데이터
predictions = model.predict(new_data)

# 예측 결과 출력
for prediction in predictions:
    if prediction > 0.5:
        print("복숭아")
    else:
        print("사과")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}