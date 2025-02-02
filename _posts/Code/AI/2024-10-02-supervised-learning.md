---
title: "[AI] 지도 학습(Supervised Learning)의 기본 개념 정리(Python 샘플코드 포함)"
excerpt: Supervised Learning

categories:
  - AI
tags:
  - [AI, 지도 학습, Supervised Learning]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 지도 학습(Supervised Learning)의 개념
---
지도 학습은 마치 선생님이 학생에게 정답을 알려주면서 가르치는 것과 같습니다. <br>
즉, 입력 데이터(Input Data)와 그에 대한 정답(Label 또는 Target)이 함께 제공되는 데이터를 사용하여 모델을 학습시키는 방식입니다. 모델은 주어진 입력 데이터와 정답 사이의 관계를 학습하여, 새로운 입력 데이터가 주어졌을 때 정답을 예측할 수 있게 됩니다. <br>
마치 시험 문제를 풀기 전에 모의고사 문제를 풀어보는 것과 같습니다. 
모의고사 문제와 정답을 통해 문제 유형을 익히고 실전 시험에서 좋은 성적을 거둘 수 있도록 준비하는 것과 같은 원리입니다.
<br><br>

![Supervised-learning](https://github.com/user-attachments/assets/583d7ce2-06ef-4f35-b580-5e2ba672e0ef)
(출처 : https://www.geeksforgeeks.org/supervised-unsupervised-learning/)<br><br>


### 지도 학습(Supervised Learning)의 종류
---
지도 학습은 크게 두 가지 유형으로 나눌 수 있습니다.

* 분류 (Classification): 입력 데이터를 미리 정의된 여러 개의 클래스(Class) 중 하나로 분류하는 문제입니다. 예를 들어, 이메일이 스팸인지 아닌지 분류하는 문제, 사진 속의 동물이 고양이인지 개인지 분류하는 문제 등이 분류 문제에 해당합니다.
* 회귀 (Regression): 입력 데이터에 대해 연속적인 숫자 값을 예측하는 문제입니다. 예를 들어, 집의 크기, 위치, 건축 연도 등의 정보를 이용하여 집 가격을 예측하는 문제, 날씨 정보를 이용하여 내일의 기온을 예측하는 문제 등이 회귀 문제에 해당합니다.

<br><br>

### 지도 학습(Supervised Learning)의 과정
---
지도 학습(Supervised Learning)은 일반적으로 다음과 같은 과정을 거칩니다.

1. 데이터 수집 (Data Collection): 학습에 필요한 입력 데이터와 정답 데이터를 수집합니다. 
```python
import pandas as pd

data = pd.read_csv("data.csv")
X = data[["feature1", "feature2", "feature3"]]
y = data["target"]

print("입력 데이터:")
print(X.head())
print("\n정답 데이터:")
print(y.head())
```
<br>

2. 데이터 전처리 (Data Preprocessing): 수집된 데이터를 정제하고 필요한 형태로 가공합니다. 예를 들어, 누락된 값을 채우거나, 텍스트 데이터를 숫자로 변환하는 등의 작업을 수행합니다.이 단계는 모델의 성능에 큰 영향을 미치므로 매우 중요합니다.
* 결측치 처리 (Handling Missing Values - Python)
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler

# 결측치 확인 및 처리
print("\n결측치 확인:")
print(X.isnull().sum())
X.fillna(X.mean(), inplace=True) # 결측치를 평균값으로 채우는 예시

# 문자형 데이터를 숫자로 변환 (One-Hot Encoding)
X = pd.get_dummies(X, columns=["feature3"])
print("\nOne-Hot Encoding 후 데이터:")
print(X.head())

# 데이터 스케일링
scaler = StandardScaler()
X_scaled_np = scaler.fit_transform(X.values)
X_scaled = pd.DataFrame(X_scaled_np, index=X.index, columns=X.columns)
print("\n스케일링 후 데이터:")
print(X_scaled.head())
```
<br>

3. 모델 선택 (Model Selection): 문제 유형에 적합한 학습 모델을 선택합니다. 예를 들어, 분류 문제에는 로지스틱 회귀, 서포트 벡터 머신, 의사 결정 트리 등의 모델을 사용할 수 있고, 회귀 
문제에는 선형 회귀, 다항 회귀 등의 모델을 사용할 수 있습니다.
* 분류 모델(Classification Model Selection)
  ```python
  from sklearn.linear_model import LogisticRegression
  from sklearn.svm import SVC
  from sklearn.tree import DecisionTreeClassifier

  # 로지스틱 회귀 모델
  model_lr = LogisticRegression()

  # 서포트 벡터 머신 모델
  model_svc = SVC()

  # 의사 결정 트리 모델
  model_dt = DecisionTreeClassifier()
  ```

* 회귀 모델(Regression Model Selection)
  ```python
  from sklearn.linear_model import LinearRegression
  from sklearn.linear_model import Ridge
  from sklearn.preprocessing import PolynomialFeatures
  
  model_linear = LinearRegression()  # 선형 회귀 (직선 형태의 관계 모델링)
  model_ridge = Ridge(alpha=1.0)  # Ridge 회귀 (L2 정규화로 과적합 방지)
  poly = PolynomialFeatures(degree=2)  # 다항 회귀를 위한 전처리
  ```
<br>

4. 모델 학습 (Model Training): 준비된 데이터를 사용하여 모델을 학습시킵니다. 
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2, random_state=42)

model_lr.fit(X_train, y_train) # 분류 모델 학습
model_linear.fit(X_train, y_train) # 회귀 모델 학습
```
<br>

5. 모델 평가 (Model Evaluation): 학습된 모델의 성능을 평가합니다. 새로운 데이터를 사용하여 모델의 예측 정확도를 측정합니다.
```python
from sklearn.metrics import accuracy_score, mean_squared_error

y_pred_lr = model_lr.predict(X_test)
accuracy = accuracy_score(y_test, y_pred_lr)
print(f"\n로지스틱 회귀 정확도: {accuracy}")

y_pred_linear = model_linear.predict(X_test)
mse = mean_squared_error(y_test, y_pred_linear)
print(f"선형 회귀 평균 제곱 오차: {mse}")
```
<br>

* 정확도(Accuracy): 분류 모델의 성능을 평가하는 지표로, 전체 예측 중 정답을 맞춘 비율을 나타냅니다.
* 평균 제곱 오차(Mean Squared Error, MSE): 회귀 모델의 성능을 평가하는 지표로, 예측값과 실제값의 차이의 제곱 평균을 나타냅니다. 값이 작을수록 모델의 성능이 좋습니다.

<br>

6. 모델 배포 (Model Deployment): 평가 결과가 만족스러우면 모델을 실제 서비스에 배포합니다.
```python
import joblib
import numpy as np

# 모델 저장
joblib.dump(model_lr, "logistic_regression_model.pkl")

# 모델 불러오기
loaded_model = joblib.load("logistic_regression_model.pkl")

# 새로운 데이터에 대한 예측 (One-hot encoding 적용)
new_data = pd.DataFrame({'feature1': [1], 'feature2': [2], 'feature3': ['A']})
new_data = pd.get_dummies(new_data, columns=["feature3"])
new_data_scaled = pd.DataFrame(scaler.transform(new_data), index=new_data.index, columns=new_data.columns)
prediction = loaded_model.predict(new_data_scaled)
print("\n새로운 데이터 예측:", prediction)
```


<br><br>

### 지도 학습(Supervised Learning)의 활용 분야
---
* 이미지 인식: 사진 속의 객체 인식, 얼굴 인식 등
* 자연어 처리: 텍스트 분류, 감성 분석, 기계 번역 등
* 의료: 질병 진단, 환자 분류 등
* 금융: 주가 예측, 신용 평가 등

<br><br> 

## 예시
---
아래는 Python의 scikit-learn 라이브러리를 사용하여 간단한 선형 회귀 모델을 학습시키는 예시 코드입니다.<br>
x 값이 증가함에 따라 y 값이 대략적으로 증가하는 관계를 학습하는 간단한 선형 회귀 모델을 보여줍니다. 실제 데이터는 이보다 훨씬 복잡하며, 다양한 전처리 과정과 모델 튜닝이 필요합니다.<br>

```python
import numpy as np
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

# 입력 데이터 (x) 와 정답 데이터 (y)
x = np.array([[1], [2], [3], [4], [5]])
y = np.array([2, 4, 5, 4, 5])

# 선형 회귀 모델 생성
model = LinearRegression()

# 모델 학습
model.fit(x, y)

# 새로운 입력 데이터에 대한 예측
new_x = np.array([[6]])
predicted_y = model.predict(new_x)
print(f"\n예측 결과: {predicted_y}")

# 학습 데이터 및 예측 결과 시각화
plt.scatter(x, y, label="Training Data")
plt.plot(x, model.predict(x), color='red', label="Linear Regression")
plt.scatter(new_x, predicted_y, marker='x', s=100, c='green', label="Prediction")
plt.xlabel("x")
plt.ylabel("y")
plt.legend()
plt.show()

print(f"기울기 (coef_): {model.coef_}")
print(f"절편 (intercept_): {model.intercept_}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}