---
title: "[AI] 준지도 학습(Semi-Supervised Learning)의 기본 개념 정리(Python 샘플코드 포함)"
excerpt: Semisupervised Learning

categories:
  - AI
tags:
  - [AI, 준지도 학습, Semisupervised Learning]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 준지도 학습(Semi-Supervised Learning)의 개념
---
준지도 학습은 지도 학습과 비지도 학습의 중간 형태라고 볼 수 있습니다. 즉, 레이블(정답)이 있는 데이터와 레이블이 없는 데이터가 혼합된 데이터를 사용하여 모델을 학습시키는 방식입니다. 현실 세계의 많은 문제에서 레이블이 있는 데이터는 얻기 어렵거나 비용이 많이 드는 반면, 레이블이 없는 데이터는 상대적으로 풍부하게 존재합니다. 준지도 학습은 이러한 상황에서 유용하게 사용될 수 있습니다. 마치 선생님이 모든 문제의 정답을 알려주는 것이 아니라, 몇몇 문제의 정답만 알려주고 나머지는 학생들이 스스로 풀어보도록 유도하는 것과 같습니다. 주어진 몇 가지 정답을 통해 문제 해결의 방향을 파악하고, 나머지 문제들을 풀면서 학습 능력을 향상시키는 방식입니다.
<br><br>

![ProposedSemisupervisedLearningProcess](https://github.com/user-attachments/assets/5a711221-aabb-49f3-ad29-20950b64b703)
(출처 : https://www.geeksforgeeks.org/ml-semi-supervised-learning/)<br><br>


### 준지도 학습(Semi-Supervised Learning)이 필요한 이유
---
* 레이블링 비용 문제: 모든 데이터에 레이블을 붙이는 것은 시간과 비용이 많이 소요되는 작업입니다. 특히 이미지 인식, 자연어 처리 등 복잡한 문제에서는 전문가의 수작업이 필요하기 때문에 더욱 그렇습니다.
* 풍부한 비레이블 데이터 활용: 현실 세계에는 레이블이 없는 데이터가 훨씬 많습니다. 준지도 학습은 이러한 풍부한 데이터를 활용하여 모델의 성능을 향상시킬 수 있습니다.
* 지도 학습의 한계 극복: 레이블이 부족한 상황에서 지도 학습만으로는 좋은 성능을 내기 어렵습니다. 준지도 학습은 이러한 한계를 극복하는 데 도움이 될 수 있습니다.

<br><br>

### 준지도 학습(Semi-Supervised Learning)의 과정
---


1. 자기 학습 (Self-Training)
자기 학습은 비교적 간단한 준지도 학습 방법으로, 레이블된 데이터로 학습된 모델을 사용하여 레이블되지 않은 데이터에 가짜 레이블(Pseudo-Label)을 부여하고, 이를 학습 데이터에 추가하여 모델을 재학습시키는 과정을 반복합니다.

```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import make_classification
from sklearn.metrics import accuracy_score

# 가상 데이터 생성
X, y = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, random_state=42)
df = pd.DataFrame(X, columns=['Feature1', 'Feature2'])
df['Target'] = y

# 레이블이 있는 데이터와 없는 데이터 분리 (10%만 레이블 존재)
X_labeled, X_unlabeled, y_labeled, y_unlabeled = train_test_split(X, y, test_size=0.9, random_state=42)

# 초기 모델 학습 (레이블된 데이터만 사용)
initial_model = LogisticRegression()
initial_model.fit(X_labeled, y_labeled)

# 레이블되지 않은 데이터에 대한 예측 및 신뢰도 계산
pseudo_labels = initial_model.predict(X_unlabeled)
probabilities = initial_model.predict_proba(X_unlabeled)

# 신뢰도가 높은 데이터 선택 (예: 확률이 0.9 이상인 경우)
high_confidence_indices = np.where(np.max(probabilities, axis=1) >= 0.9)[0]
X_pseudo = X_unlabeled[high_confidence_indices]
y_pseudo = pseudo_labels[high_confidence_indices]

# 가짜 레이블이 부여된 데이터를 학습 데이터에 추가
X_extended = np.concatenate((X_labeled, X_pseudo))
y_extended = np.concatenate((y_labeled, y_pseudo))

# 확장된 데이터로 모델 재학습
final_model = LogisticRegression()
final_model.fit(X_extended, y_extended)

# 전체 데이터에 대한 예측 및 정확도 측정
y_pred = final_model.predict(X)
accuracy = accuracy_score(y, y_pred)
print(f"전체 데이터에 대한 정확도: {accuracy}")
```
<br>

2. 공동 학습 (Co-Training)
공동 학습은 두 개 이상의 모델(또는 뷰)을 사용하여 학습을 진행합니다. 데이터의 서로 다른 특징 집합을 사용하는 여러 개의 모델을 학습시켜, 서로의 예측 결과를 활용하여 레이블되지 않은 데이터에 대한 학습을 돕는 방법입니다.

   1. 데이터를 두 가지 특징 집합으로 나눕니다 (예: 이미지의 색상 특징과 모양 특징).
   2. 각 특징 집합에 대해 별도의 분류기(Classifier)를 학습시킵니다.
   3. 각 분류기는 레이블되지 않은 데이터에 대해 예측을 수행합니다.
   4. 두 분류기의 예측이 일치하는 데이터에 대해 가짜 레이블을 부여하고, 각 분류기의 학습 데이터에 추가합니다.
   5. 위 과정을 반복합니다.

3. 그래프 기반 방법 (Graph-Based Methods)
그래프 기반 방법은 데이터를 그래프 형태로 표현하고 데이터 포인트를 노드로, 데이터 간의 유사성을 엣지로 연결합니다. 레이블이 있는 데이터의 레이블을 그래프를 통해 인접한 레이블이 없는 데이터로 전파하는 방법입니다.

```python
from sklearn.semi_supervised import LabelSpreading

# 레이블이 없는 데이터의 레이블을 -1로 설정 (LabelSpreading에 필요)
y_unlabeled = np.full(X_unlabeled.shape[0], -1)
X_semi = np.concatenate((X_labeled, X_unlabeled))
y_semi = np.concatenate((y_labeled, y_unlabeled))

label_spread = LabelSpreading(kernel='knn', alpha=0.8)
label_spread.fit(X_semi, y_semi)
y_pred = label_spread.predict(X)
accuracy_all = accuracy_score(y, y_pred)
print(f"레이블 전파 후 전체 데이터에 대한 정확도: {accuracy_all}")
```

<br>

4. 생성 모델 기반 방법 (Generative Models)
데이터의 확률 분포를 학습하여 레이블되지 않은 데이터의 레이블을 추정하는 방법입니다. 가우시안 혼합 모델(Gaussian Mixture Model, GMM) 등이 대표적인 예시입니다.
 
   1. 레이블된 데이터와 레이블되지 않은 데이터를 사용하여 GMM을 학습합니다.
   2. 학습된 GMM을 사용하여 각 데이터 포인트가 어떤 클러스터에 속할 확률을 계산합니다.
   3. 레이블된 데이터의 클러스터 정보를 활용하여 레이블되지 않은 데이터에 가짜 레이블을 부여합니다.

<br><br>

### 준지도 학습(Semi-Supervised Learning)의 활용 분야
---
* 이미지 분류: 소량의 레이블된 이미지와 대량의 레이블되지 않은 이미지를 사용하여 이미지 분류 모델 학습
* 자연어 처리: 텍스트 분류, 감성 분석 등에서 레이블되지 않은 텍스트 데이터를 활용
* 의료 영상 분석: 의료 영상 데이터는 레이블링에 전문 지식이 필요하므로, 준지도 학습을 통해 학습 효율을 높일 수 있음
* 웹 문서 분류: 웹 페이지들을 주제별로 분류하는 작업

<br><br> 

## 예시
---
Python의 scikit-learn 라이브러리를 사용하여 간단한 자기 학습을 구현하는 예시 코드입니다. 완벽한 자기 학습 구현은 아니며, 개념적인 이해를 돕기 위한 간단한 예시입니다.
<br>

```python
import numpy as np
from sklearn.semi_supervised import LabelSpreading # 레이블 전파 알고리즘 사용 (자기학습의 한 종류로 간주 가능)
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 가상 데이터 생성 (1000개 샘플, 2개의 특징)
X, y = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, random_state=42)

# 레이블이 있는 데이터와 없는 데이터 분리 (10%만 레이블 존재)
X_labeled, X_unlabeled, y_labeled, _ = train_test_split(X, y, test_size=0.9, random_state=42)

# 레이블이 없는 데이터의 레이블을 -1로 설정
y_unlabeled = np.full(X_unlabeled.shape[0], -1)

# 레이블이 있는 데이터와 없는 데이터 합치기
X_semi = np.concatenate((X_labeled, X_unlabeled))
y_semi = np.concatenate((y_labeled, y_unlabeled))

# LabelSpreading 모델 생성 및 학습
label_spread = LabelSpreading(kernel='knn', alpha=0.8) # alpha는 레이블 전파 강도 조절
label_spread.fit(X_semi, y_semi)

# 모든 데이터에 대한 예측
y_pred = label_spread.predict(X)

# 원래 레이블이 있던 데이터에 대한 정확도 측정 (비교를 위해)
y_true_labeled = y[:len(y_labeled)]
y_pred_labeled = y_pred[:len(y_labeled)]
accuracy = accuracy_score(y_true_labeled, y_pred_labeled)
print(f"레이블 데이터에 대한 정확도: {accuracy}")

# 전체 데이터에 대한 정확도 측정
accuracy_all = accuracy_score(y, y_pred)
print(f"전체 데이터에 대한 정확도: {accuracy_all}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}