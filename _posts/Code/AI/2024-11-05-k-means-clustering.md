---
title: "[AI] K-평균 클러스터링(K-Means Clustering)의 기본 개념 정리(Python 샘플코드 포함)"
excerpt: K-Means Clustering

categories:
  - AI
tags:
  - [AI, K-평균 클러스터링, K-평균, K-Means Clustering, K Means]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## K-평균 클러스터링(K-Means Clustering)의 개념
---
머신러닝의 중요한 비지도 학습 알고리즘 중 하나인 K-평균 클러스터링(K-Means Clustering)은 주어진 데이터를 K개의 클러스터(cluster), 즉 그룹으로 나누는 알고리즘입니다. 여기서 "K"는 사용자가 미리 지정해야 하는 클러스터의 개수를 의미합니다. 이 알고리즘의 목표는 각 클러스터 내의 데이터들 사이의 거리는 가깝게, 서로 다른 클러스터에 속한 데이터들 사이의 거리는 멀게 만드는 것입니다. 마치 학교에서 학생들을 키 순서대로 여러 그룹으로 나누는 것과 유사합니다. 키가 비슷한 학생들끼리 같은 그룹에 속하게 되고, 키 차이가 많이 나는 학생들은 다른 그룹에 속하게 되는 것이죠.

좀 더 정확히 말하면, K-평균 알고리즘은 각 클러스터의 중심(centroid)과 클러스터에 속한 데이터 포인트들 간의 거리 제곱합을 최소화하는 방식으로 작동합니다.
<br><br>

![Image](https://github.com/user-attachments/assets/531e66d0-e255-486f-b855-ca5c9075ed45)
(출처 : https://www.geeksforgeeks.org/k-means-clustering-introduction/)<br><br>


### K-평균 클러스터링의 작동 원리
---
K-평균 클러스터링은 다음과 같은 단계를 반복합니다.

1. 초기 중심(Centroid) 선택: K개의 클러스터 중심을 임의로 선택합니다. 일반적으로 데이터 포인트 중에서 K개를 무작위로 선택하거나, 데이터를 K개의 영역으로 나누어 각 영역의 중심을 선택합니다.
2. 클러스터 할당: 각 데이터 포인트를 가장 가까운 중심에 할당합니다. 이때, 유클리드 거리(Euclidean distance)를 사용하여 거리를 계산합니다.
3. 중심 재계산: 각 클러스터의 중심을 해당 클러스터에 속한 데이터 포인트들의 평균값으로 갱신합니다.
4. 2~3단계를 클러스터의 중심이 더 이상 변하지 않거나, 미리 정해진 반복 횟수에 도달할 때까지 반복합니다.

<br>

### K-평균 클러스터링의 장단점
---
#### 장점
* 구현이 간단하고 계산 속도가 빠릅니다.
* 대용량 데이터에도 적용 가능합니다.

#### 단점
* 클러스터의 개수 K를 미리 지정해야 합니다. 적절한 K 값을 선택하는 것이 중요합니다.
* 초기 중심 선택에 따라 결과가 달라질 수 있습니다.
* 클러스터가 원형이 아닌 경우 잘 작동하지 않을 수 있습니다.
* 이상치(outlier)에 민감합니다.

<br>

### K 값 선택 방법
---
적절한 K 값을 선택하는 것은 K-평균 클러스터링에서 매우 중요합니다. 대표적인 방법은 다음과 같습니다.

* 엘보우 방법 (Elbow Method): K 값을 변화시키면서 각 K 값에 대한 클러스터 내 제곱합(Within-Cluster Sum of Squares, WCSS)을 계산합니다. WCSS 값이 급격히 감소하다가 완만하게 변하는 지점(엘보우 포인트)의 K 값을 최적의 K 값으로 선택합니다.
* 실루엣 분석 (Silhouette Analysis): 각 데이터 포인트의 실루엣 계수를 계산하여 클러스터링의 적합성을 평가합니다. 실루엣 계수는 -1부터 1 사이의 값을 가지며, 1에 가까울수록 클러스터링이 잘 되었다는 것을 의미합니다.

<br>

### K-평균 클러스터링(K-Means Clustering)의 과정
---

예시를 위해 공통으로 사용할 2차원 가상 데이터를 생성합니다.

가상데이터 생성
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs

# 가상 데이터 생성 (3개의 클러스터)
X, y = make_blobs(n_samples=300, centers=3, random_state=42, cluster_std=0.6)

# 데이터 시각화
plt.scatter(X[:, 0], X[:, 1])
plt.title("Generated Data")
plt.show()
```
<br>

1. 초기 중심(Centroid) 선택 (Initial Centroid Selection)<br>
K개의 클러스터 중심을 임의로 선택합니다. 여기서는 데이터 포인트 중에서 K개를 무작위로 선택하는 방법을 사용하겠습니다. k-means++ 초기화는 sklearn의 KMeans에서 기본으로 사용되므로, 여기서는 기본적인 무작위 선택을 보여드리겠습니다.
```python
import random

def initialize_centroids(X, k):
    """데이터 X에서 k개의 중심을 무작위로 선택합니다."""
    indices = random.sample(range(len(X)), k) # 중복 없이 k개 선택
    centroids = X[indices]
    return centroids

k = 3 # 클러스터 개수
initial_centroids = initialize_centroids(X, k)

print("초기 중심:", initial_centroids)

# 초기 중심 시각화
plt.scatter(X[:, 0], X[:, 1])
plt.scatter(initial_centroids[:, 0], initial_centroids[:, 1], marker='x', s=200, c='red', label='Initial Centroids')
plt.title("Initial Centroids")
plt.legend()
plt.show()
```
<br>

2. 클러스터 할당 (Cluster Assignment)<br>
각 데이터 포인트를 가장 가까운 중심에 할당합니다. 유클리드 거리를 사용하여 거리를 계산합니다.
```python
def assign_to_clusters(X, centroids):
    """각 데이터 포인트를 가장 가까운 중심에 할당합니다."""
    distances = np.sqrt(((X - centroids[:, np.newaxis])**2).sum(axis=2)) # 각 데이터 포인트와 중심 사이의 거리 계산 (브로드캐스팅 활용)
    cluster_assignments = np.argmin(distances, axis=0) # 가장 가까운 중심의 인덱스 반환
    return cluster_assignments

cluster_assignments = assign_to_clusters(X, initial_centroids)

print("클러스터 할당 결과:", cluster_assignments)

# 클러스터 할당 결과 시각화
plt.scatter(X[:, 0], X[:, 1], c=cluster_assignments)
plt.scatter(initial_centroids[:, 0], initial_centroids[:, 1], marker='x', s=200, c='red', label='Initial Centroids')
plt.title("Cluster Assignment")
plt.legend()
plt.show()
```
<br>

3. 중심 재계산 (Centroid Recomputation)<br>
각 클러스터의 중심을 해당 클러스터에 속한 데이터 포인트들의 평균값으로 갱신합니다.
```python
def recompute_centroids(X, cluster_assignments, k):
    """각 클러스터의 중심을 재계산합니다."""
    new_centroids = np.array([X[cluster_assignments == i].mean(axis=0) for i in range(k)]) # 각 클러스터의 평균 계산
    return new_centroids

new_centroids = recompute_centroids(X, cluster_assignments, k)

print("새로운 중심:", new_centroids)

# 새로운 중심 시각화
plt.scatter(X[:, 0], X[:, 1], c=cluster_assignments)
plt.scatter(new_centroids[:, 0], new_centroids[:, 1], marker='x', s=200, c='red', label='New Centroids')
plt.title("Centroid Recomputation")
plt.legend()
plt.show()
```
<br>

4. 상기 과정 반복<br>
위의 클러스터 할당과 중심 재계산 단계를 중심이 더 이상 변하지 않거나, 미리 정해진 반복 횟수에 도달할 때까지 반복합니다. 이것이 K-평균 알고리즘의 핵심입니다.
<br><br>

### K-평균 클러스터링(K-Means Clustering)의 활용 분야
---
* 고객 세분화 (Customer Segmentation)
  * 마케팅 분야에서 고객들을 유사한 특징을 가진 그룹으로 나누어 맞춤형 마케팅 전략을 수립하는 데 사용됩니다. 예를 들어, 구매 이력, 인구 통계 정보, 웹사이트 방문 기록 등을 이용하여 고객들을 분류하고, 각 그룹에 맞는 광고나 프로모션을 제공할 수 있습니다.
  * 고객의 특성을 파악하여 새로운 상품을 개발하거나, 고객 만족도를 높이는 데에도 활용될 수 있습니다.

* 이미지 분할 (Image Segmentation)
  * 이미지를 여러 개의 영역으로 나누는 작업에 사용됩니다. 예를 들어, 의료 영상 분석에서 종양이나 장기 영역을 분리하거나, 위성 사진 분석에서 토지 이용 현황을 파악하는 데 활용될 수 있습니다.
  * 이미지의 픽셀들을 색상, 밝기, 질감 등의 특징에 따라 클러스터링하여 각 영역을 대표하는 색상값을 추출할 수 있습니다. 이를 통해 이미지의 특징을 파악하거나, 이미지의 색상을 조작하는 등의 작업을 수행할 수 있습니다.

* 데이터 압축 (Data Compression)
  * 데이터의 크기를 줄이는 데 사용될 수 있습니다. 예를 들어, 이미지나 오디오 데이터를 클러스터링하여 각 클러스터를 대표하는 값만 저장함으로써 데이터 용량을 줄일 수 있습니다.
  * 벡터 양자화(Vector Quantization) 기법에서 K-평균 클러스터링이 활용됩니다.

* 이상 탐지 (Anomaly Detection)
  * 정상적인 데이터 패턴에서 벗어난 이상치를 탐지하는 데 사용될 수 있습니다. 예를 들어, 신용 카드 사기 탐지, 네트워크 침입 탐지 등에 활용될 수 있습니다.
  * 데이터를 클러스터링한 후, 클러스터에서 멀리 떨어진 데이터 포인트를 이상치로 간주할 수 있습니다.

* 문서 분류 (Document Clustering)
  * 문서들을 주제별로 분류하는 데 사용됩니다. 예를 들어, 뉴스 기사, 학술 논문, 웹 페이지 등을 주제에 따라 자동으로 분류할 수 있습니다.
  * 문서의 단어 빈도, TF-IDF 등의 특징을 이용하여 문서를 클러스터링합니다.

* 추천 시스템 (Recommender Systems)
  * 사용자들의 선호도를 분석하여 상품이나 콘텐츠를 추천하는 데 사용될 수 있습니다. 예를 들어, 영화 추천, 음악 추천, 상품 추천 등에 활용될 수 있습니다.
  * 사용자들의 구매 패턴, 평점 등을 이용하여 사용자를 클러스터링하고, 같은 클러스터에 속한 사용자들에게 유사한 상품을 추천할 수 있습니다.

* 유전자 데이터 분석 (Gene Expression Data Analysis)
  * 유전자 발현 데이터를 분석하여 유사한 유전자들을 그룹으로 나누는 데 사용됩니다. 이를 통해 유전자 기능 연구, 질병 진단 등에 활용될 수 있습니다.

* 검색 엔진 (Search Engines)
  * 검색 결과를 클러스터링하여 사용자에게 더 관련성 높은 결과를 제공하는 데 사용될 수 있습니다.

<br><br> 

## 예시
---
Python의 scikit-learn 라이브러리를 사용하여 K-평균 클러스터링을 수행하는 예시 코드입니다.
<br>

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
from sklearn.metrics import silhouette_score

# 가상 데이터 생성 (3개의 클러스터)
X, y = make_blobs(n_samples=300, centers=3, random_state=42)

# 엘보우 방법으로 최적의 K 값 찾기
wcss = []
for i in range(1, 11):
    kmeans = KMeans(n_clusters=i, init='k-means++', max_iter=300, n_init=10, random_state=0)
    kmeans.fit(X)
    wcss.append(kmeans.inertia_)
plt.plot(range(1, 11), wcss)
plt.title('Elbow Method')
plt.xlabel('Number of clusters')
plt.ylabel('WCSS')
plt.show()

# K-평균 모델 생성 (클러스터 개수: 3)
kmeans = KMeans(n_clusters=3, init='k-means++', max_iter=300, n_init=10, random_state=0)

# 모델 학습
kmeans.fit(X)

# 클러스터 레이블 예측
labels = kmeans.predict(X)

# 결과 시각화
plt.scatter(X[:, 0], X[:, 1], c=labels)
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], marker='x', s=200, c='red') # 중심점 표시
plt.title("K-means Clustering")
plt.show()

# 실루엣 점수 계산
silhouette_avg = silhouette_score(X, labels)
print(f"실루엣 점수: {silhouette_avg}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}