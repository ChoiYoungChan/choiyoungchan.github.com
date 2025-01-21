---
title:  "[AI] 딥 러닝(Deep Learning)핵심 정리"
excerpt: Deep Learning

categories:
  - AI
tags:
  - [AI, DL, Deep Learning, 딥 러닝]

toc: true
toc_sticky: true
 
date: 2024-03-21
last_modified_at: 2024-03-21
---

## Deep Learning 개념
---
딥러닝(Deep Learning)은 인공 신경망을 기반으로 하여 데이터 속에서 복잡한 패턴을 학습하고 예측하는 인공지능 기술입니다. <br>
인간의 뇌 신경망을 모방하여 다층 구조의 신경망을 통해 데이터를 처리하며, 방대한 양의 데이터를 학습하여 고도의 추론과 판단이 가능합니다.

### 처리방식
* 순전파(Forward Propagation): 입력 데이터가 신경망을 따라 한 층씩 전파되면서 출력 값을 생성하는 과정입니다. 각 층에서 가중치와 편향을 곱하고 활성화 함수를 거쳐 다음 층으로 전달됩니다.

![Backpropagation](https://github.com/user-attachments/assets/09d0b465-6745-451d-8d8b-a3617830af75) <출처 geeksforgeeks><br> <br>


* 역전파(Backpropagation): 출력 값과 실제 값의 차이(오차)를 계산하고, 이 오차를 역으로 전파하여 각 층의 가중치와 편향을 수정하는 과정입니다. 이를 통해 모델이 오차를 줄이고 정확도를 높여나갑니다.

![Forward_Propagation](https://github.com/user-attachments/assets/7a9234fc-c73a-4702-84c0-43ba3e78c87f) <출처 geeksforgeeks><br><br><br>

  
### 알고리즘
* 경사 하강법(Gradient Descent): 오차 함수를 최소화하는 방향으로 모델의 파라미터를 업데이트하는 최적화 알고리즘입니다.  
* 확률적 경사 하강법(Stochastic Gradient Descent): 전체 데이터를 한 번에 사용하는 대신, 일부 데이터를 무작위로 추출하여 학습하는 방식으로, 학습 속도를 향상시킵니다.
* 미니 배치 경사 하강법(Mini-batch Gradient Descent): 전체 데이터를 작은 단위(미니 배치)로 나누어 학습하는 방식으로, 메모리 효율성과 학습 안정성을 높입니다.

![Mini-batch_Gradient_Descent](https://github.com/user-attachments/assets/e86a40d7-d8fd-49a8-a839-3943e491f13b) <출처 alwaysai><br> <br>

  
### 모델 종류
* 인공 신경망(Artificial Neural Network, ANN): 가장 기본적인 신경망 모델로, 다층 퍼셉트론(Multi-Layer Perceptron, MLP)이 대표적입니다
* 합성곱 신경망(Convolutional Neural Network, CNN): 이미지 처리에 특화된 신경망으로, 필터를 이용하여 이미지의 특징을 추출합니다.
* 순환 신경망(Recurrent Neural Network, RNN): 시퀀스 데이터(문장, 시계열 데이터 등) 처리에 특화된 신경망으로, LSTM(Long Short-Term Memory)과 GRU(Gated Recurrent Unit)가 대표적입니다.
* Transformer: 자연어 처리 분야에서 뛰어난 성능을 보이는 신경망 모델로, Attention Mechanism을 기반으로 하여 문맥을 효과적으로 파악합니다. (예: BERT, GPT)
* Generative Adversarial Network (GAN): 이미지, 음성 등의 데이터를 생성하는 데 사용되는 신경망으로, 생성 모델과 판별 모델이 서로 경쟁하며 학습합니다.


### 장단점
##### 장점
* 복잡한 패턴 학습: 방대한 양의 데이터에서 복잡한 패턴을 학습하여 고난도의 문제를 해결할 수 있습니다.
* 자동 특징 추출: 수동으로 특징을 설계할 필요 없이 데이터에서 자동으로 유용한 특징을 추출합니다.
* 다양한 분야 적용: 이미지 인식, 자연어 처리, 음성 인식 등 다양한 분야에 적용될 수 있습니다.
* 지속적인 발전: 딥러닝 기술은 빠르게 발전하고 있으며, 새로운 알고리즘과 모델이 지속적으로 개발되고 있습니다.

##### 단점
* 많은 데이터 필요: 딥러닝 모델은 많은 양의 데이터를 필요로 하며, 데이터가 부족할 경우 성능이 저하될 수 있습니다.
* 높은 계산 비용: 복잡한 모델을 학습하기 위해 많은 연산 자원이 필요합니다.
* 블랙박스 문제: 딥러닝 모델의 의사 결정 과정을 이해하기 어려워, 신뢰성에 대한 의문이 제기될 수 있습니다.
* 과적합 문제: 훈련 데이터에 과도하게 적합되어 새로운 데이터에 대한 일반화 성능이 저하될 수 있습니다.

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}