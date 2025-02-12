---
title:  "[AI] 서포트 벡터 머신(Support Vector Machine)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Support Vector Machine

categories:
  - AI
tags:
  - [AI, 서포트 벡터 머신, Support Vector Machine, SVM]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 서포트 벡터 머신(Support Vector Machine)의 개념
---
Machine Learning을 배우면서 **"어떤 기준으로 데이터를 나누어야 가장 깔끔하게 분류할 수 있을까?"** 라는 고민을 해본 적 있으시다면 Support Vector Machine(SVM)은 바로 이 질문에 대한 해답을 제시하는 강력한 기계 학습 알고리즘입니다.

SVM은 데이터를 가장 효과적으로 분류하는 최적의 경계면을 찾는 것을 목표로 합니다. 마치 여러 개의 점들을 가장 깔끔하게 나누는 선을 긋는 것과 같다고 생각하면 됩니다. SVM은 1990년대에 개발되었지만, 여전히 많은 분야에서 뛰어난 성능을 보여주는 인기 있는 알고리즘입니다.
<br><br>

![Image](https://github.com/user-attachments/assets/27e9f52d-0de2-42ac-8e41-bcfb13efc842)
(출처 : https://hands-on.cloud/svm-python-tutorial/)<br><br>


### 서포트 벡터 머신(Support Vector Machine)의 특징
---
뛰어난 분류 성능: SVM은 복잡한 데이터도 효과적으로 분류할 수 있습니다. 특히 고차원 데이터에서 강점을 보입니다.
일반화 능력: SVM은 학습 데이터에만 의존하지 않고, 새로운 데이터에도 잘 적용되는 능력을 가지고 있습니다.
최적의 경계면: SVM은 데이터를 가장 효과적으로 나눌 수 있는 최적의 경계면을 찾습니다.
다양한 커널 함수: SVM은 다양한 커널 함수를 사용하여 비선형적인 데이터를 처리할 수 있습니다.
<br><br>

### 서포트 벡터 머신(Support Vector Machine)의 종류
---
* 선형 SVM: 데이터를 선형적으로 분류할 수 있는 경우 사용합니다.
비선형 SVM: 데이터를 비선형적으로 분류해야 하는 경우 사용합니다. 커널 함수를 사용하여 데이터를 고차원 공간으로 매핑하여 선형 분류를 수행합니다.
소프트 마진 SVM: 데이터가 완벽하게 선형으로 분류되지 않는 경우, 일부 데이터 포인트를 허용하는 마진을 사용합니다.
하드 마진 SVM: 데이터가 완벽하게 선형으로 분류되는 경우 사용합니다.
<br><br>

### 서포트 벡터 머신(Support Vector Machine)의 장단점
---
#### 장점
* 높은 분류 정확도: 다양한 데이터셋에서 뛰어난 분류 성능을 보여줍니다.
* 과적합 방지: 최대 마진을 가지는 경계면을 찾기 때문에 과적합(overfitting)을 방지할 수 있습니다.
* 다양한 커널 함수: 다양한 커널 함수를 사용하여 비선형적인 데이터를 처리할 수 있습니다.

#### 단점
* 계산 비용: 대규모 데이터셋의 경우 계산 비용이 많이 소요될 수 있습니다.
* 커널 선택: 적절한 커널 함수를 선택하는 것이 중요합니다.
* 블랙박스 모델: 모델의 작동 방식을 명확하게 설명하기 어렵습니다.
<br><br>

### 서포트 벡터 머신(Support Vector Machine)의 작동 과정
---

1. 데이터 표현: 데이터를 벡터 공간에 점으로 표현합니다. 각 점은 데이터의 특징을 나타냅니다.
2. 최적의 경계면 찾기: 데이터를 두 개의 클래스로 나누는 경계면을 찾습니다. 이때, 각 클래스와 경계면 사이의 거리를 최대한 멀리 떨어뜨리는 **최대 마진(maximum margin)**을 가지는 경계면을 찾습니다.
3. 서포트 벡터: 경계면과 가장 가까운 데이터 포인트들을 **서포트 벡터(support vector)**라고 합니다. 이 서포트 벡터들이 경계면의 위치와 방향을 결정합니다.
4. 커널 함수: 데이터가 선형적으로 분류되지 않을 경우, **커널 함수(kernel function)**를 사용하여 데이터를 고차원 공간으로 매핑합니다. 이 고차원 공간에서 선형 분류를 수행합니다.
<br><br>

[SVM 작동 과정 샘플 코드 (Python, scikit-learn 라이브러리 활용)]
```python
from sklearn import svm
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 데이터 준비
X = [[0, 0], [1, 1], [2, 0], [3, 1]] # 특징 데이터
y = [0, 1, 0, 1] # 레이블 (0 또는 1)

# 데이터 분할
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# SVM 모델 생성 및 학습
model = svm.SVC(kernel='linear') # 선형 커널 사용
model.fit(X_train, y_train)

# 예측
y_pred = model.predict(X_test)

# 평가
accuracy = accuracy_score(y_test, y_pred)
print("Accuracy:", accuracy)
```
<br><br>

### 서포트 벡터 머신(Support Vector Machine)사용 시 주의사항
---
* 데이터 전처리: SVM은 데이터의 스케일에 민감하므로, 데이터를 정규화하거나 표준화하는 것이 좋습니다.
* 커널 선택: 적절한 커널 함수를 선택하는 것이 중요합니다. 데이터의 특성에 따라 다양한 커널 함수를 시도해보고 최적의 커널을 선택해야 합니다.
* 하이퍼파라미터 튜닝: SVM 모델의 성능을 높이기 위해 하이퍼파라미터(C, gamma 등)를 적절하게 튜닝해야 합니다.
<br><br>

## 예시 코드
---
```python
from sklearn import svm
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 데이터 준비
X = [[0, 0], [1, 1], [2, 0], [3, 1]] # 특징 데이터
y = [0, 1, 0, 1] # 레이블 (0 또는 1)

# 데이터 분할
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# 다양한 커널을 사용하여 SVM 모델 생성 및 학습
kernels = ['linear', 'rbf', 'poly', 'sigmoid']
for kernel in kernels:
    model = svm.SVC(kernel=kernel)
    model.fit(X_train, y_train)

    # 예측
    y_pred = model.predict(X_test)

    # 평가
    accuracy = accuracy_score(y_test, y_pred)
    print(f"{kernel} 커널 사용 시 정확도: {accuracy}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}