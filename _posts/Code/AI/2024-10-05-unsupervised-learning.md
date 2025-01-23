---
title:  "[AI] 비지도학습(Unsupervised Learning)의 기본 개념 정리(Python 샘플코드 포함)"
excerpt: Unsupervised Learning

categories:
  - AI
tags:
  - [AI, 비지도학습, Unsupervised Learning]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 비지도학습(Unsupervised Learning)의 개념
---
비지도 학습은 지도 학습과는 달리, 입력 데이터에 대한 정답(Label 또는 Target)이 제공되지 않은 상태에서 데이터 자체의 패턴이나 구조를 학습하는 방식입니다. 마치 아이가 그림책을 보면서 그림의 형태나 색깔을 스스로 인지하고 분류하는 것과 같습니다. 정답을 알려주는 선생님 없이, 데이터 자체를 탐색하며 숨겨진 규칙이나 의미를 찾아내는 것이죠. 마치 탐험가가 새로운 대륙을 탐험하며 지도를 만들어나가는 것과 유사합니다. 주어진 데이터만으로 데이터를 분석하고 새로운 지식을 발견하는 것이 비지도 학습의 핵심입니다.
<br><br>

![Unsupervised-learning](https://github.com/user-attachments/assets/f8fc93ed-b6fd-4485-b2ac-aec61ffa17d3)
(출처 : https://www.geeksforgeeks.org/unsupervised-learning/)<br><br>


### 비지도학습(Unsupervised Learning)의 종류
---
비지도 학습은 크게 다음과 같은 유형으로 나눌 수 있습니다.

* 군집화 (Clustering): 유사한 데이터들을 그룹(클러스터)으로 묶는 작업입니다. 예를 들어, 고객 데이터를 분석하여 유사한 구매 패턴을 가진 고객들을 그룹으로 나누는 것, 문서들을 주제별로 분류하는 것 등이 군집화 문제에 해당합니다.
* 차원 축소 (Dimensionality Reduction): 고차원의 데이터를 저차원으로 축소하는 작업입니다. 데이터의 중요한 특징을 유지하면서 데이터의 크기를 줄여 계산 효율성을 높이거나 시각화를 용이하게 하는 데 사용됩니다. 예를 들어, 이미지 데이터를 분석할 때 픽셀 단위의 고차원 데이터를 주요 특징만 추출하여 저차원으로 표현하는 것이 차원 축소에 해당합니다.
* 연관 규칙 학습 (Association Rule Learning): 데이터 간의 연관성 또는 규칙을 찾는 작업입니다. 예를 들어, 장바구니 분석에서 "맥주를 산 고객은 안주도 함께 사는 경향이 있다"와 같은 규칙을 발견하는 것이 연관 규칙 학습에 해당합니다.

<br><br>

### 비지도학습(Unsupervised Learning)의 활용 분야
---
비지도 학습은 다양한 분야에서 활용되고 있습니다.

* 고객 세분화 (Customer Segmentation): 고객 데이터를 분석하여 마케팅 전략 수립
* 추천 시스템 (Recommender Systems): 사용자들의 구매 패턴을 분석하여 상품 추천
* 이상 감지 (Anomaly Detection): 비정상적인 데이터 패턴 감지
* 이미지 압축 및 특징 추출: 이미지 데이터의 용량을 줄이거나 주요 특징 추출
* 자연어 처리: 문서 분류, 토픽 모델링 등

<br><br>

### 비지도학습(Unsupervised Learning)의 과정
---
비지도 학습은 일반적으로 다음과 같은 과정을 거칩니다.


1. 데이터 수집 (Data Collection): 학습에 필요한 입력 데이터를 수집합니다. 이번에는 scikit-learn에서 제공하는 가상 데이터 생성 함수를 사용하여 예시를 간단하게 만들어 보겠습니다. 
   실제 프로젝트에서는 다양한 출처에서 데이터를 수집해야 합니다.<br><br>
  * 가상 데이터 생성 (Python)
    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    from sklearn.datasets import make_blobs
    
    # 가상 데이터 생성 (3개의 클러스터)
    X, y = make_blobs(n_samples=300, centers=3, random_state=42, cluster_std=0.6)

    # DataFrame으로 변환
    df = pd.DataFrame(X, columns=['Feature1', 'Feature2'])

    # 데이터 시각화
    plt.scatter(df['Feature1'], df['Feature2'])
    plt.title("Generated Data")
    plt.show()

    print("생성된 데이터:")
    print(df.head())
    ```
<br>

2. 데이터 전처리 (Data Preprocessing): 수집된 데이터를 정제하고 필요한 형태로 가공합니다. 지도 학습과 마찬가지로 중요한 단계입니다.
    ```python
    from sklearn.preprocessing import StandardScaler

    # 결측치 확인 및 처리
    print("\n결측치 확인:")
    print(df.isnull().sum())
    df.fillna(df.mean(), inplace=True) # 결측치를 평균값으로 채우는 예시

    # 데이터 스케일링
    scaler = StandardScaler()
    X_scaled_np = scaler.fit_transform(df.values)
    X_scaled = pd.DataFrame(X_scaled_np, index=df.index, columns=df.columns)

    print("\n스케일링 전 데이터:")
    print(df.head())
    print("\n스케일링 후 데이터:")
    print(X_scaled.head())
    ```
<br>

3. 알고리즘 선택 (Algorithm Selection): 문제 유형에 적합한 알고리즘을 선택합니다. 
* 군집화: K-평균, DBSCAN 등
* 차원 축소: PCA, t-SNE 등
* 연관 규칙 학습: Apriori, FP-Growth 등
<br><br>

4. 모델 학습 (Model Training): 준비된 데이터를 사용하여 모델을 학습시킵니다. 모델은 데이터의 패턴이나 구조를 학습합니다.
* K-평균 군집화 (K-means Clustering - Python)
    ```python
    from sklearn.cluster import KMeans

    # K-평균 모델 생성 (클러스터 개수: 3)
    kmeans = KMeans(n_clusters=3, random_state=42)

    # 모델 학습
    kmeans.fit(scaled_features)

    # 클러스터 레이블 예측
    kmeans_labels = kmeans.predict(scaled_features)

    df['KMeans_Cluster'] = kmeans_labels
    print(df.head())

    # 결과 시각화
    plt.scatter(df['Feature1'], df['Feature2'], c=df['KMeans_Cluster'], alpha=0.5)
    plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], marker='x', s=200, c='red', label='Centroids')
    plt.title("K-means Clustering")
    plt.legend()
    plt.show()
    ```

* DBSCAN 군집화 (DBSCAN Clustering - Python)
  ```python
  from sklearn.cluster import DBSCAN

  # DBSCAN 모델 생성 (eps: 반경, min_samples: 최소 샘플 수)
  dbscan = DBSCAN(eps=0.5, min_samples=5)

  # 모델 학습
  dbscan.fit(scaled_features)

  # 클러스터 레이블 예측
  dbscan_labels = dbscan.fit_predict(scaled_features)

  df['DBSCAN_Cluster'] = dbscan_labels

  print(df.head())

  # 결과 시각화 (노이즈는 -1로 표시)
  plt.scatter(df['Feature1'], df['Feature2'], c=df['DBSCAN_Cluster'], alpha=0.5)
  plt.title("DBSCAN Clustering")
  plt.show()
  ```
<br><br>

5. 결과 분석 및 평가 (Result Analysis and Evaluation): 학습된 모델의 결과를 분석하고 평가합니다. 비지도 학습은 정답이 제공되지 않기 때문에, 지도 학습처럼 명확한 평가 지표를 사용하기 어렵습니다. 데이터의 시각화, 도메인 전문가의 판단 등을 통해 결과를 평가합니다.
   * 군집화 결과 시각화 (Clustering Result Visualization - Python)
    ```python
    import matplotlib.pyplot as plt

    # 클러스터 레이블 예측
    labels = kmeans.predict(X_scaled)

    # 결과 시각화
    plt.scatter(X_scaled.iloc[:, 0], X_scaled.iloc[:, 1], c=labels) # 스케일링된 데이터 사용
    plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], marker='x', s=200, c='red') # 중심점 표시
    plt.title("K-means Clustering")
    plt.show()
    ```
<br>

  * 차원 축소 결과 시각화 (PCA Result Visualization - Python)
    ```python
    import matplotlib.pyplot as plt

    # 차원 축소된 데이터 시각화
    plt.scatter(X_reduced[:, 0], X_reduced[:, 1])
    plt.title("PCA Dimensionality Reduction")
    plt.xlabel("Principal Component 1")
    plt.ylabel("Principal Component 2")
    plt.show()
    ```
<br>

  * 실루엣 분석 (Silhouette Analysis - Python) (군집화 평가)
    ```python
    from sklearn.metrics import silhouette_score

    silhouette_avg = silhouette_score(X_scaled, labels)
    print(f"실루엣 점수: {silhouette_avg}")
    ```

<br><br>


## 예시
---
Python의 scikit-learn 라이브러리를 사용하여 간단한 K-평균 군집화를 수행하는 예시 코드입니다.
make_blobs 함수를 사용하여 3개의 클러스터를 가진 가상 데이터를 생성하고, K-평균 알고리즘을 사용하여 데이터를 3개의 클러스터로 군집화합니다. 결과를 시각화하여 클러스터링 결과를 확인할 수 있습니다.
<br> 

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs

# 가상 데이터 생성 (3개의 클러스터)
X, y = make_blobs(n_samples=300, centers=3, random_state=42)

# K-평균 모델 생성 (클러스터 개수: 3)
kmeans = KMeans(n_clusters=3, random_state=42)

# 모델 학습
kmeans.fit(X)

# 클러스터 레이블 예측
labels = kmeans.predict(X)

# 결과 시각화
plt.scatter(X[:, 0], X[:, 1], c=labels)
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], marker='x', s=200, c='red') # 중심점 표시
plt.title("K-means Clustering")
plt.show()

print("클러스터 중심점:", kmeans.cluster_centers_)
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}