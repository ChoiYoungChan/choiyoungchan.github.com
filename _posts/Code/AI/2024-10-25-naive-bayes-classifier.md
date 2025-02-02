---
title: "[AI] 나이브 베이즈 분류기(Naive Bayes Classifier)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Naive Bayes Classifier

categories:
  - AI
tags:
  - [AI, 나이브 베이즈 분류기, Naive Bayes Classifier]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 나이브 베이즈 분류기(Naive Bayes Classifier)의 개념
---
머신러닝의 중요한 분류 알고리즘 중 하나인 나이브 베이즈 분류기는 베이즈 정리(Bayes' theorem)에 기반한 확률적 분류 알고리즘입니다. 특히 텍스트 분류, 스팸 메일 필터링, 감성 분석 등 다양한 분야에서 효과적으로 사용됩니다. "나이브(Naive)"라는 이름은 이 알고리즘이 모든 특성(feature)이 서로 독립적이라고 가정하는 데서 유래합니다. 이 가정이 실제로는 다소 단순화된 가정이지만, 그럼에도 불구하고 나이브 베이즈 분류기는 많은 경우에 좋은 성능을 보여줍니다.
<br><br>

![Image](https://github.com/user-attachments/assets/8c69a417-4267-4c2a-a5c5-2b790f31c0e6)
(출처 : https://www.linkedin.com/pulse/understanding-naive-bayes-machine-learning-fundamental-aritra-pain/)<br><br>


### 베이즈 정리 (Bayes' theorem)
---
나이브 베이즈 분류기는 주어진 입력 데이터 x가 특정 클래스 c에 속할 확률 P(c|x)를 계산합니다. 베이즈 정리를 적용하면 다음과 같이 됩니다.

P(c|x) = [P(x|c) * P(c)] / P(x)

여기서 각 용어의 의미는 다음과 같습니다.

* P(c|x): 사후 확률(posterior probability). 입력 데이터 x가 주어졌을 때 클래스 c일 확률. 우리가 구하고자 하는 값입니다.
* P(x|c): 가능도(likelihood). 클래스 c가 주어졌을 때 입력 데이터 x가 나타날 확률.
* P(c): 사전 확률(prior probability). 클래스 c가 나타날 확률.
* P(x): 증거(evidence). 입력 데이터 x가 나타날 확률.
x는 여러 개의 특성 (x₁, x₂, ..., xₙ)으로 이루어져 있다고 가정합니다. 나이브 베이즈 분류기는 모든 특성이 서로 독립적이라고 가정하므로, P(x|c)는 다음과 같이 분해될 수 있습니다.

P(x|c) = P(x₁|c) * P(x₂|c) * ... * P(xₙ|c)

따라서, 최종적인 식은 다음과 같습니다.

P(c|x) = [P(c) * Π P(xᵢ|c)] / P(x) (i = 1 to n)

분류를 수행할 때는 모든 클래스 c에 대해 P(c|x)를 계산하고, 가장 높은 확률을 가진 클래스를 선택합니다. 분모 P(x)는 모든 클래스에 대해 동일하므로, 비교할 때는 분자 부분만 계산하면 됩니다.

<br><br>

### 나이브 베이즈 분류기의 종류
---
1. 가우시안 나이브 베이즈 (Gaussian Naive Bayes)<br>
특성이 연속적인 값을 가지며, 가우시안 분포(정규 분포)를 따른다고 가정할 때 사용합니다. 예를 들어, 키, 몸무게, 시험 점수 등 연속적인 값을 가지는 데이터에 적합합니다.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score

# 가상 데이터 생성 (2개의 클래스, 연속적인 특징)
np.random.seed(0)
X = np.concatenate([np.random.normal(0, 1, (100, 2)), np.random.normal(5, 1, (100, 2))])
y = np.concatenate([np.zeros(100), np.ones(100)])

# 데이터를 학습 데이터와 테스트 데이터로 분리
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# 가우시안 나이브 베이즈 모델 생성 및 학습
gnb = GaussianNB()
gnb.fit(X_train, y_train)

# 예측 및 정확도 측정
y_pred = gnb.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f"가우시안 나이브 베이즈 정확도: {accuracy}") # 출력 예시: 0.9833333333333333

# 결정 경계 시각화
x_min, x_max = X[:, 0].min() - 1, X[:, 0].max() + 1
y_min, y_max = X[:, 1].min() - 1, X[:, 1].max() + 1
xx, yy = np.meshgrid(np.arange(x_min, x_max, 0.1), np.arange(y_min, y_max, 0.1))
Z = gnb.predict(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)
plt.contourf(xx, yy, Z, alpha=0.4)
plt.scatter(X[:, 0], X[:, 1], c=y, s=20, edgecolor='k')
plt.title("Gaussian Naive Bayes Decision Boundary")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.show()
```
<br>

2. 다항 나이브 베이즈 (Multinomial Naive Bayes)<br>
특성이 이산적인 값을 가지며, 다항 분포를 따른다고 가정할 때 사용합니다. 주로 텍스트 분류 (단어 빈도수 등)에 적합합니다.

```python
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics import accuracy_score

# 텍스트 데이터 예시
corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?",
    "This is not a document."
]
labels = [0, 0, 0, 0, 1]  # 0: 문서, 1: 문서 아님

# 텍스트 데이터를 숫자 벡터로 변환 (CountVectorizer 사용)
vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)

# 데이터를 학습 데이터와 테스트 데이터로 분리
X_train, X_test, y_train, y_test = train_test_split(X, labels, test_size=0.3, random_state=42)

# 다항 나이브 베이즈 모델 생성 및 학습
mnb = MultinomialNB()
mnb.fit(X_train, y_train)

# 예측 및 정확도 측정
y_pred = mnb.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f"다항 나이브 베이즈 정확도: {accuracy}") # 출력 예시: 1.0
```
<br>

3. 베르누이 나이브 베이즈 (Bernoulli Naive Bayes)<br>
특성이 이진 값(0 또는 1)을 가지며, 베르누이 분포를 따른다고 가정할 때 사용합니다. 텍스트 분류에서 단어의 출현 여부 (존재하면 1, 존재하지 않으면 0)를 나타낼 때 유용합니다.
```python
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import BernoulliNB
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics import accuracy_score

# 텍스트 데이터 예시 (이전 예제와 동일)
corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?",
    "This is not a document."
]
labels = [0, 0, 0, 0, 1]

# 텍스트 데이터를 이진 벡터로 변환 (CountVectorizer의 binary=True 옵션 사용)
vectorizer = CountVectorizer(binary=True)
X = vectorizer.fit_transform(corpus)

# 데이터를 학습 데이터와 테스트 데이터로 분리
X_train, X_test, y_train, y_test = train_test_split(X, labels, test_size=0.3, random_state=42)

# 베르누이 나이브 베이즈 모델 생성 및 학습
bnb = BernoulliNB()
bnb.fit(X_train, y_train)

# 예측 및 정확도 측정
y_pred = bnb.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f"베르누이 나이브 베이즈 정확도: {accuracy}") # 출력 예시: 1.0
```

<br><br>

### 나이브 베이즈 분류기(Naive Bayes Classifier)의 장단점
---
#### 장점
* 구현이 간단하고 계산 속도가 빠릅니다. 베이즈 정리를 기반으로 비교적 간단한 계산을 수행하기 때문에, 다른 복잡한 알고리즘에 비해 학습 및 예측 속도가 빠릅니다.
* 비교적 적은 데이터로도 좋은 성능을 보일 수 있습니다. 특히, 특성들이 독립이라는 가정이 어느 정도 만족되는 경우, 적은 데이터로도 효율적인 학습이 가능합니다.
* 고차원 데이터에 효과적입니다. 특성의 수가 많은 데이터셋에서도 계산 효율성을 유지하며 좋은 성능을 보일 수 있습니다.
* 텍스트 분류에 특히 강점을 보입니다. 단어 빈도수와 같은 이산적인 특성을 다루는 데 적합하여, 스팸 메일 필터링, 문서 분류 등에 효과적으로 사용됩니다.

#### 단점
* 특성 간의 독립성을 가정하기 때문에, 특성 간의 상관 관계가 강한 경우에는 성능이 저하될 수 있습니다. 예를 들어, "뜨겁다"와 "커피"라는 단어는 함께 등장할 확률이 높지만, 나이브 베이즈는 이 둘을 독립적인 특성으로 간주하여 실제 의미를 제대로 반영하지 못할 수 있습니다.
* 학습 데이터에 없는 특성 값이 테스트 데이터에 나타나는 경우, 확률이 0이 되어 문제가 발생할 수 있습니다 (제로 빈도 문제). 예를 들어, 학습 데이터에 "스마트폰"이라는 단어가 한 번도 등장하지 않았는데, 테스트 데이터에 "새로운 스마트폰"이라는 문장이 나타나면, "스마트폰"의 확률이 0이 되어 전체 확률 계산에 오류가 발생할 수 있습니다.
* 연속형 데이터의 경우, 데이터의 분포를 가정해야 합니다. 가우시안 나이브 베이즈의 경우 정규 분포를 가정하는데, 실제 데이터가 정규 분포를 따르지 않는 경우 성능이 저하될 수 있습니다.
<br><br> 

### 제로 빈도 문제 해결: 라플라스 스무딩 (Laplace Smoothing)
---
제로 빈도 문제는 라플라스 스무딩(또는 가산 스무딩)을 통해 해결할 수 있습니다. 라플라스 스무딩은 모든 특성의 빈도에 작은 값(보통 1)을 더해줌으로써 확률이 0이 되는 것을 방지합니다. 이렇게 하면 학습 데이터에 없는 특성이 나타나더라도 확률이 0이 되지 않고, 모델의 일반화 성능을 향상시킬 수 있습니다.
<br><br> 

## 예시
---
Python의 scikit-learn 라이브러리를 사용하여 가우시안 나이브 베이즈 분류기를 학습시키는 예시 코드입니다.
<br>

```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score

# 가상 데이터 생성
X = np.array([
    [1, 2], [1.5, 1.8], [5, 8], [8, 8], [1, 0.6], [9, 11]
])
y = np.array([0, 0, 1, 1, 0, 1]) # 0과 1 두 개의 클래스

# 데이터를 학습 데이터와 테스트 데이터로 분리
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# 가우시안 나이브 베이즈 모델 생성
gnb = GaussianNB()

# 모델 학습
gnb.fit(X_train, y_train)

# 테스트 데이터에 대한 예측
y_pred = gnb.predict(X_test)

# 정확도 측정
accuracy = accuracy_score(y_test, y_pred)
print(f"정확도: {accuracy}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}