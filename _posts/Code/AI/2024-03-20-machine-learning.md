---
title:  "[AI] 머신러닝(Machine Learning) 핵심 정리"
excerpt: Machine Learning

categories:
  - AI
tags:
  - [AI, ML, 머신러닝]

toc: true
toc_sticky: true
 
date: 2024-03-20
last_modified_at: 2024-03-20
---

## Machine Learning 개념
---
머신 러닝(Machine Learning)은 컴퓨터가 명시적으로 프로그래밍되지 않고 데이터를 통해 스스로 학습하고 예측하는 능력을 갖추는 기술입니다.<br> 
즉, 컴퓨터가 데이터를 분석하고 패턴을 인식하여 새로운 데이터에 대한 예측이나 결정을 내릴 수 있도록 하는 것입니다.

### 처리방식
* 학습(Training): 알고리즘에 데이터를 입력하여 모델을 생성하는 과정입니다. 학습 데이터를 통해 모델의 파라미터를 조정하여 예측 성능을 향상시킵니다.
* 예측(Prediction): 학습된 모델에 새로운 데이터를 입력하여 결과를 예측하는 과정입니다.

  
### 알고리즘

크게 3가지 학습 방법으로 나누어집니다.
1. Supervised Learning
2. Unsupervised Learning
3. Reinforcement Learning

<br> 

![The-main-typesn](https://github.com/user-attachments/assets/1ea3f041-b851-4a55-b3a5-6fd01a540950) <출처 researchgate><br><br> 


* 지도 학습(Supervised Learning): 입력 데이터와 정답(레이블) 쌍으로 이루어진 학습 데이터를 사용하여 모델을 학습시키는 방법입니다.
  * 분류(Classification): 데이터를 여러 클래스로 분류하는 문제 (예: 스팸 메일 분류, 이미지 분류)
  * 회귀(Regression): 연속적인 값을 예측하는 문제 (예: 주택 가격 예측, 온도 예측)
  
![Supervised_Learning](https://github.com/user-attachments/assets/ff46d475-0bdd-4284-bf56-1c9849de76c0) <출처 edushots><br><br> 

* 비지도 학습(Unsupervised Learning): 정답이 없는 데이터를 사용하여 데이터 속의 숨겨진 구조나 패턴을 찾는 방법입니다.
  * 클러스터링(Clustering): 유사한 특징을 가진 데이터를 그룹으로 묶는 문제
  * 차원 축소(Dimensionality Reduction): 고차원 데이터를 저차원 공간으로 변환하여 데이터를 시각화하거나 분석하는 문제

![Unsupervised_Learning](https://github.com/user-attachments/assets/9ad9d52f-03c2-4861-9783-6af35b41832c) <출처 edushots><br><br> 

* 강화 학습(Reinforcement Learning): 에이전트가 환경과 상호작용하며 보상을 최대화하는 행동을 학습하는 방법입니다.

![Reinforcement_Learning](https://github.com/user-attachments/assets/ce9b10ff-4a84-48b0-88ac-f331bb13b734) <출처 researchgate><br><br> 

  
### 모델 종류
* 선형 회귀(Linear Regression): 입력 변수와 출력 변수 사이의 선형 관계를 모델링하는 알고리즘
* 로지스틱 회귀(Logistic Regression): 분류 문제에 사용되는 알고리즘으로, 시그모이드 함수를 사용하여 확률 값을 예측합니다.
* 결정 트리(Decision Tree): 의사 결정 규칙을 나무 형태로 표현하여 데이터를 분류하거나 예측하는 알고리즘
* 랜덤 포레스트(Random Forest): 다수의 결정 트리를 결합하여 예측 성능을 향상시키는 알고리즘
* 서포트 벡터 머신(Support Vector Machine, SVM): 데이터를 분류하는 최적의 초평면을 찾는 알고리즘
* k-최근접 이웃(k-Nearest Neighbors, k-NN): 새로운 데이터 포인트를 가장 가까운 k개의 이웃 데이터 포인트의 클래스로 분류하는 알고리즘


### 장단점
##### 장점
* 데이터 기반 의사 결정: 방대한 데이터를 분석하여 정확한 예측과 의사 결정을 지원합니다.
* 자동화: 반복적인 작업을 자동화하여 생산성을 향상시킵니다.
* 새로운 패턴 발견: 데이터 속에 숨겨진 새로운 패턴을 발견하여 새로운 지식을 얻을 수 있습니다.

##### 단점
* 데이터 의존성: 학습 데이터의 질이 모델 성능에 큰 영향을 미칩니다.
* 과적합 문제: 훈련 데이터에 과도하게 적합되어 새로운 데이터에 대한 일반화 성능이 저하될 수 있습니다.
* 해석 어려움: 일부 모델은 복잡하여 내부 작동 원리를 이해하기 어렵습니다.

### 딥러닝과 머신 러닝의 관계
딥러닝은 머신 러닝의 한 분야입니다.<br> 
딥러닝은 인공 신경망을 기반으로 하여 더 복잡한 문제를 해결할 수 있도록 발전했습니다. <br> 
머신 러닝은 딥러닝 외에도 다양한 알고리즘과 기법을 포함합니다.


![ml-whitepaper-1](https://github.com/user-attachments/assets/49e29589-a7f9-42a8-99f9-9fb197f9f925) <출처 nvidia>

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}