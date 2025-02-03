---
title:  "[AI] K-NN 알고리즘(K nearest Neighbors)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: K nearest Neighbors

categories:
  - AI
tags:
  - [AI, K-NN 알고리즘, K nearest Neighbors, KNN]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## K-NN 알고리즘(K nearest Neighbors)의 개념
---
K-NN 알고리즘은 가장 가까운 이웃 K개를 찾아, 이웃들의 정보를 이용하여 새로운 데이터의 종류를 예측하는 알고리즘입니다. 여기서 'K'는 사용자가 지정해야 하는 이웃의 개수를 의미합니다.

K-NN은 직관적이고 이해하기 쉬운 알고리즘입니다. 예를 들어, 새로운 학생의 키와 몸무게를 알고 있을 때, 이 학생과 가장 비슷한 K명의 학생들을 찾아 그들의 성별을 확인하여 새로운 학생의 성별을 예측할 수 있습니다.
<br><br>

![Image](https://github.com/user-attachments/assets/c42b0cbf-29be-4a31-89ff-11e27d11b7a1)
(출처 : https://www.ibm.com/think/topics/knn)
<br><br>


### K-NN 알고리즘(K nearest Neighbors)의 장단점
---
#### 장점
* 단순하고 이해하기 쉽습니다: 알고리즘의 작동 방식이 직관적이고 이해하기 쉽습니다.
* 구현이 용이합니다: 비교적 간단한 코드로 구현할 수 있습니다.
* 다양한 문제에 적용 가능합니다: 분류, 회귀 등 다양한 문제에 적용할 수 있습니다.

#### 단점
* 계산 비용이 높습니다: 모든 데이터와의 거리를 계산해야 하므로 데이터의 크기가 클 경우 계산 비용이 높아집니다.
* 이상치에 민감합니다: 이상치가 존재할 경우 예측 결과에 큰 영향을 미칠 수 있습니다.
* 최적의 K 값을 선택해야 합니다: K 값에 따라 성능이 달라지므로 적절한 K 값을 찾아야 합니다.

<br><br>

### K값 선택 방법
---
적절한 K 값을 선택하는 것은 K-NN 알고리즘의 성능에 큰 영향을 미칩니다. 일반적으로 다음과 같은 방법을 사용하여 최적의 K 값을 찾습니다.

* 교차 검증 (Cross-validation): 데이터를 여러 개의 부분 집합으로 나누어 각 부분 집합을 번갈아 가며 학습 및 검증에 사용하고, 평균 검증 성능이 가장 높은 K 값을 선택합니다.
* 엘보우 방법 (Elbow Method): K 값을 변화시키면서 모델의 성능을 평가하고, 성능이 급격히 감소하는 지점을 최적의 K 값으로 선택합니다.

<br><br>

### K-NN 알고리즘(K nearest Neighbors)의 작동 원리
---

K-NN 알고리즘은 다음과 같은 단계를 거쳐 작동합니다. <br><br>

1. 거리 계산: 새로운 데이터와 기존 데이터의 모든 점들 사이의 거리를 계산합니다. 거리는 유클리드 거리, 맨해튼 거리 등 다양한 방법을 사용할 수 있습니다.<br><br>
  
  * 유클리드 거리 (Euclidean Distance)<br>
  유클리드 거리는 2차원 또는 다차원 공간에서 두 점 사이의 직선 거리를 의미합니다. 가장 흔히 사용되는 거리 계산 방식으로, 우리에게 가장 익숙한 개념입니다.<br><br>
  
    계산 방법 <br>
    두 점 A(x1, y1)와 B(x2, y2) 사이의 유클리드 거리는 다음과 같이 계산합니다.<br><br>
    ```
    유클리드 거리 = √((x2 - x1)^2 + (y2 - y1)^2)
    ```

    다차원 공간에서는 각 차원의 좌표 차이를 제곱하여 더한 후 제곱근을 취합니다.<br><br>
    ```
    유클리드 거리 = √((x2 - x1)^2 + (y2 - y1)^2 + ... + (xn - x1)^2)
    ```

    특징
    * 차원(Dimension)에 민감합니다: 데이터의 차원이 증가할수록 유클리드 거리는 기하급수적으로 커집니다. 이를 **차원의 저주(Curse of Dimensionality)**라고 합니다. 따라서 고차원 데이터의 경우 유클리드 거리를 사용하는 것에 신중해야 합니다.
    * 스케일(Scale)에 민감합니다: 데이터의 각 특징(feature)의 스케일이 다를 경우 유클리드 거리가 큰 영향을 받습니다. 예를 들어, 키는 cm 단위로 측정하고 몸무게는 kg 단위로 측정하는 경우, 키의 변화는 유클리드 거리에 거의 영향을 미치지 못할 수 있습니다. 따라서 데이터를 표준화(Standardization)하거나 정규화(Normalization)하여 스케일을 맞춰주는 것이 중요합니다.
    * 이상치(Outlier)에 민감합니다: 이상치는 유클리드 거리를 크게 증가시킬 수 있습니다. 따라서 이상치를 제거하거나 처리하는 것이 필요할 수 있습니다.
    * 밀도(Density)에 무관합니다: 데이터의 밀도 분포에 상관없이 두 점 사이의 직선 거리만 계산합니다. 따라서 밀도가 낮은 지역에서도 정확한 거리를 측정할 수 있습니다.
    <br><br>

  * 맨해튼 거리 (Manhattan Distance)<br>
  맨해튼 거리는 두 점 사이의 거리를 각 좌표축 방향으로의 거리 합으로 계산하는 방식입니다. 마치 도시의 블록처럼, 가로와 세로 방향으로만 이동할 수 있다고 가정하고 계산하는 거리입니다.<br><br>
  계산 방법<br>
    두 점 A(x1, y1)와 B(x2, y2) 사이의 맨해튼 거리는 다음과 같이 계산합니다.<br><br>
    ```
    맨해튼 거리 = |x1 - x2| + |y1 - y2|
    ```

    특징
    * 유클리드 거리에 비해 계산량이 적습니다.
    * 데이터의 특징이 각 축에 독립적인 경우에 유용합니다.
    * 이상치에 덜 민감합니다.
    <br><br>

  * 민코프스키 거리 (Minkowski Distance)<br>
    민코프스키 거리는 유클리드 거리와 맨해튼 거리를 일반화한 거리 계산 방식입니다. p 값을 조절하여 다양한 거리를 계산할 수 있습니다.<br><br>
      
    계산 방법<br>
      두 점 A(x1, y1)와 B(x2, y2) 사이의 민코프스키 거리는 다음과 같이 계산합니다.<br><br>
      ```
      민코프스키 거리 = (|x1 - x2|^p + |y1 - y2|^p)^(1/p)
      ```
      * p = 2: 유클리드 거리
      * p = 1: 맨해튼 거리
      <br><br>

      특징
      * p 값에 따라 다양한 거리를 표현할 수 있습니다.
      * 유클리드 거리와 맨해튼 거리를 포함하는 일반적인 개념입니다.
  
  <br><br>

아래 샘플코드에서는 유클리드 거리를 사용하겠습니다.
```python
def euclidean_distance(x1, x2):
    """유클리드 거리 계산 함수"""
    return np.sqrt(np.sum((x1 - x2)**2))

distances = []
for i in range(len(X)):
    distance = euclidean_distance(new_data, X[i])
    distances.append((distance, i)) # (거리, 인덱스) 튜플 저장

print("각 데이터와의 거리:", distances)
```
<br><br>

2. K 이웃 선택: 계산된 거리를 기준으로 가장 가까운 K개의 이웃을 선택합니다.
```python
k = 3 # 이웃의 개수
distances.sort() # 거리를 기준으로 정렬
neighbors = distances[:k] # 가장 가까운 K개의 이웃 선택

print("가장 가까운", k, "개의 이웃:", neighbors)
```
<br><br>

3. 클래스 예측: 선택된 이웃들의 클래스 중 가장 많은 클래스를 새로운 데이터의 클래스로 예측합니다.

```python
neighbor_labels = [y[i] for distance, i in neighbors] # 이웃들의 클래스 레이블
prediction = max(set(neighbor_labels), key=neighbor_labels.count) # 가장 많은 클래스 선택

print("예측된 클래스:", prediction)
```
<br>

전체 코드 및 시각화
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier

# 가상 데이터 생성
X = np.array([[1, 1], [1.5, 1.5], [2, 2], [8, 8], [9, 9], [8.5, 8.5]])
y = np.array([0, 0, 0, 1, 1, 1])

# 새로운 데이터 (분류할 데이터)
new_data = np.array([[5, 5]])

# K-NN 모델 생성 및 학습 (scikit-learn 사용)
knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(X, y)

# 예측
prediction = knn.predict(new_data)

# 시각화
plt.scatter(X[:, 0], X[:, 1], c=y)
plt.scatter(new_data[:, 0], new_data[:, 1], marker='x', s=200, c='red', label=f'New Data (Class {prediction[0]})')
plt.title("K-NN Classification")
plt.legend()
plt.show()
```

<br><br>

### K-NN 알고리즘(K nearest Neighbors)의 활용 분야
---
* 추천 시스템 (Recommender Systems)
  * 영화 추천: 사용자가 시청한 영화 데이터를 기반으로, K-NN 알고리즘을 사용하여 사용자와 가장 유사한 취향을 가진 다른 사용자를 찾습니다. 그리고 이들이 높게 평가한 영화를 사용자에게 추천합니다.
  * 상품 추천: 온라인 쇼핑몰에서 사용자가 구매한 상품 이력을 바탕으로, 유사한 구매 패턴을 가진 다른 사용자의 구매 상품을 추천합니다.
  * 뉴스 추천: 사용자가 읽은 뉴스 기사를 분석하여, 사용자와 유사한 관심사를 가진 다른 사용자가 읽은 뉴스 기사를 추천합니다.

* 이미지 인식 (Image Recognition)
  * 얼굴 인식: 얼굴 이미지 데이터를 학습하고, 새로운 얼굴 이미지와 가장 가까운 K개의 얼굴 이미지를 찾아 얼굴을 식별합니다.
  * 문자 인식: 손글씨나 인쇄된 문자 이미지를 학습하고, 새로운 문자 이미지와 가장 가까운 K개의 문자 이미지를 찾아 문자를 인식합니다.
  * 객체 인식: 이미지 속 객체의 특징을 추출하여 학습하고, 새로운 이미지 속 객체와 가장 가까운 K개의 객체를 찾아 객체를 인식합니다.

* 자연어 처리 (Natural Language Processing)
  * 텍스트 분류: 텍스트 데이터를 학습하고, 새로운 텍스트와 가장 가까운 K개의 텍스트를 찾아 텍스트의 주제나 감성을 분류합니다.
  * 문서 요약: 문서의 내용을 학습하고, 문서와 가장 가까운 K개의 문장을 찾아 문서를 요약합니다.
  * 챗봇: 사용자 질문과 가장 유사한 K개의 질문을 찾아, 해당 질문에 대한 답변을 제공합니다.

* 의료 분야 (Medical Field)
  * 질병 진단: 환자의 증상 데이터를 학습하고, 새로운 환자 데이터와 가장 가까운 K명의 환자 데이터를 찾아 질병을 진단합니다.
  * 유전자 분석: 유전자 데이터를 학습하고, 새로운 유전자 데이터와 가장 가까운 K개의 유전자 데이터를 찾아 유전자의 기능을 분석합니다.
  * 환자 분류: 환자의 특성 데이터를 학습하고, 새로운 환자 데이터와 가장 가까운 K명의 환자를 찾아 환자를 분류합니다.

* 금융 분야 (Financial Field)
  * 신용 평가: 고객의 신용 데이터를 학습하고, 새로운 고객 데이터와 가장 가까운 K명의 고객 데이터를 찾아 고객의 신용도를 평가합니다.
  * 주가 예측: 주가 데이터를 학습하고, 새로운 주가 데이터와 가장 가까운 K개의 주가 데이터를 찾아 주가를 예측합니다.
  * 사기 탐지: 거래 데이터를 학습하고, 새로운 거래 데이터와 가장 가까운 K개의 거래 데이터를 찾아 사기 거래를 탐지합니다.

* 기타 분야
  * 데이터 마이닝: 데이터 속에서 유용한 정보를 찾아내는 데 활용됩니다.
  * 패턴 인식: 데이터 속에서 특정한 패턴을 찾아내는 데 활용됩니다.
  * 이상 감지: 정상적인 데이터 패턴에서 벗어난 이상 데이터를 탐지하는 데 활용됩니다.
<br><br> 

## 예시
---
아래의 샘플 코드는 Python의 scikit-learn 라이브러리를 사용하여 K-NN 알고리즘을 구현하는 간단한 예시 입니다.
<br>

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 가상 데이터 생성
X = np.array([[1, 1], [1.5, 1.5], [2, 2], [8, 8], [9, 9], [8.5, 8.5]])
y = np.array([0, 0, 0, 1, 1, 1])

# 데이터를 학습 데이터와 테스트 데이터로 분리
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# K-NN 모델 생성 (K=3)
knn = KNeighborsClassifier(n_neighbors=3)

# 모델 학습
knn.fit(X_train, y_train)

# 예측
y_pred = knn.predict(X_test)

# 정확도 측정
accuracy = accuracy_score(y_test, y_pred)
print(f"정확도: {accuracy}")

# 결과 시각화
plt.scatter(X[:, 0], X[:, 1], c=y)
plt.scatter(X_test[:, 0], X_test[:, 1], marker='x', s=200, c='red')
plt.title("K-NN Classification")
plt.show()
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}