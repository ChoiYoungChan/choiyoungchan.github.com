---
title:  "[AI] 은닉 마르코프 모델(Hidden Markov Model)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Hidden Markov Model

categories:
  - AI
tags:
  - [AI, 은닉 마르코프 모델, Hidden Markov Model]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 은닉 마르코프 모델(Hidden Markov Model)의 개념
---
은닉 마르코프 모델(HMM)은 시간에 따라 변하는 시스템을 모델링하는 확률적 모델입니다. 특히, 시스템의 상태가 직접적으로 관측되지 않고, 그 상태에 따라 발생하는 관측값(observation)을 통해서만 간접적으로 추론할 수 있을 때 유용합니다. "은닉(Hidden)"이라는 이름은 바로 이러한 숨겨진 상태를 의미합니다.

간단한 예를 들어보겠습니다. 매일 아이스크림을 얼마나 먹었는지 기록한다고 가정해 봅시다. 아이스크림 소비량은 직접 기록하기 때문에 관측 가능합니다. 반면에, 그날의 날씨는 기록하지 않았기 때문에 직접적으로 알 수 없습니다. 하지만, 날씨가 더우면 아이스크림을 더 많이 먹을 가능성이 높고, 날씨가 추우면 아이스크림을 덜 먹을 가능성이 높다는 것을 알고 있습니다. 이때, 날씨는 은닉 상태가 되고, 아이스크림 소비량은 관측값이 됩니다. HMM은 이러한 관계를 모델링하여 관측된 아이스크림 소비량을 통해 숨겨진 날씨 상태를 추론하는 데 사용될 수 있습니다. 마치 탐정이 여러 단서(관측값)를 통해 사건의 진실(은닉 상태)을 추론하는 것과 같습니다.
<br><br>

![Image](https://github.com/user-attachments/assets/c948be52-229f-4b95-bd4b-be80d686dd2f)
(출처 : https://en.wikipedia.org/wiki/Hidden_Markov_model)<br><br>

### 마르코프 가정 (Markov Assumption)
---
HMM은 마르코프 가정이라는 중요한 가정을 기반으로 합니다. 마르코프 가정은 현재 상태는 바로 이전 상태에만 의존한다는 가정입니다. 즉, 과거의 모든 상태가 현재 상태에 영향을 미치는 것이 아니라, 바로 직전 상태만이 현재 상태에 영향을 미친다고 가정합니다. 예를 들어, 오늘의 날씨는 어제의 날씨에만 영향을 받고, 그 이전의 날씨에는 직접적인 영향을 받지 않는다고 가정하는 것입니다. 마치 도미노가 바로 앞의 도미노에 의해서만 넘어지는 것과 같습니다.
<br><br>

### HMM의 구성 요소
---
HMM은 다음과 같은 요소들로 구성됩니다.

* 상태 (States): 시스템이 가질 수 있는 유한한 개수의 상태. 위 예시에서는 "더움", "추움"과 같은 날씨 상태가 됩니다.
* 관측값 (Observations): 각 상태에서 발생할 수 있는 관측 가능한 값. 위 예시에서는 아이스크림 소비량이 됩니다.
* 상태 전이 확률 (State Transition Probabilities): 한 상태에서 다른 상태로 전이할 확률. 예를 들어, "더움"에서 "추움"으로 날씨가 바뀔 확률입니다.
* 방출 확률 (Emission Probabilities): 각 상태에서 특정 관측값이 발생할 확률. 예를 들어, "더움" 상태에서 아이스크림을 많이 먹을 확률입니다.
* 초기 상태 확률 (Initial State Probabilities): 시스템이 처음 시작할 때 각 상태에 있을 확률. 예를 들어, 첫날 날씨가 "더움"일 확률입니다.
<br><br>

### HMM의 세 가지 기본 문제
---

1. 평가 (Evaluation): 주어진 HMM 파라미터(상태 전이 확률, 방출 확률, 초기 상태 확률)와 관측값 시퀀스가 주어졌을 때, 해당 관측값 시퀀스가 발생할 확률을 계산하는 문제입니다. Forward 알고리즘은 이 확률을 효율적으로 계산하는 방법입니다.<br>

```python
import numpy as np
from hmmlearn import hmm

# HMM 파라미터 설정
n_states = 2  # 상태 개수 (예: 더움, 추움)
n_observations = 3  # 관측값 개수 (예: 아이스크림 적게 먹음, 보통 먹음, 많이 먹음)

start_prob = np.array([0.6, 0.4])  # 초기 상태 확률 (첫날 더울 확률 60%, 추울 확률 40%)
trans_mat = np.array([[0.7, 0.3], [0.4, 0.6]])  # 상태 전이 확률 (더움 -> 더움 70%, 더움 -> 추움 30%, 추움 -> 더움 40%, 추움 -> 추움 60%)
emission_prob = np.array([[0.1, 0.4, 0.5], [0.6, 0.3, 0.1]])  # 방출 확률 (더울 때 적게 10%, 보통 40%, 많이 50%, 추울 때 적게 60%, 보통 30%, 많이 10%)

# HMM 모델 생성 (파라미터 직접 설정)
model = hmm.MultinomialHMM(n_components=n_states)
model.startprob_ = start_prob
model.transmat_ = trans_mat
model.emissionprob_ = emission_prob

# 관측값 시퀀스
X = np.array([[0], [1], [2]])  # 예: [적게 먹음, 보통 먹음, 많이 먹음]

# 관측값 시퀀스가 발생할 확률 계산 (평가)
logprob = model.score(X)  # 로그 확률 값 반환
probability = np.exp(logprob)  # 실제 확률 값 계산
print(f"관측값 시퀀스 발생 확률: {probability}") # 출력 예시: 0.0483

# 여러개의 관측값 시퀀스에 대한 확률 계산 (score_samples 사용)
X_multi = np.array([[0, 1, 2], [2, 1, 0]]).reshape(-1, 1)  # 여러 시퀀스를 학습시키기 위해 reshape 필요
lengths = [3, 3]  # 각 시퀀스의 길이
logprob_multi = model.score_samples(X_multi, lengths=lengths) #각 시퀀스에 대한 로그 확률 반환
probabilities_multi = np.exp(logprob_multi) #각 시퀀스에 대한 확률 값 계산
print(f"여러 관측값 시퀀스 발생 확률:\n {probabilities_multi}") # 출력 예시: [[0.0483] [0.0366]]

# 모델에서 샘플 생성
X_sampled, Z = model.sample(10)  # 10개의 시간 스텝에 대한 샘플 생성
print(f"샘플된 관측값 시퀀스:\n {X_sampled.flatten()}")
print(f"샘플된 은닉 상태 시퀀스:\n {Z}")
```
<br><br>

2. 디코딩 (Decoding): 디코딩 문제는 주어진 HMM 파라미터와 관측값 시퀀스가 주어졌을 때, 가장 가능성 높은 은닉 상태 시퀀스를 찾는 문제입니다. Viterbi 알고리즘은 이 문제를 효율적으로 해결하는 동적 프로그래밍 알고리즘입니다. 예를 들어, 아이스크림 소비량 시퀀스가 주어졌을 때, 어떤 날씨 시퀀스가 가장 가능성이 높은지 추론하는 것입니다.<br>

```python
import numpy as np
from hmmlearn import hmm

# HMM 파라미터 (위와 동일)
n_states = 2
n_observations = 3
start_prob = np.array([0.6, 0.4])
trans_mat = np.array([[0.7, 0.3], [0.4, 0.6]])
emission_prob = np.array([[0.1, 0.4, 0.5], [0.6, 0.3, 0.1]])

# HMM 모델 생성
model = hmm.MultinomialHMM(n_components=n_states)
model.startprob_ = start_prob
model.transmat_ = trans_mat
model.emissionprob_ = emission_prob

# 관측값 시퀀스 (위와 동일)
X = np.array([[0], [1], [2]])  # 예: [적게 먹음, 보통 먹음, 많이 먹음]

# 가장 가능성 높은 은닉 상태 시퀀스 찾기 (디코딩)
logprob, states = model.decode(X)
print(f"가장 가능성 높은 은닉 상태 시퀀스: {states}") # 출력 예시: [1 1 0] (추움, 추움, 더움)
print(f"최대 로그 확률: {logprob}") # 출력 예시: -4.135166540181631
```
<br>

3. 학습 (Learning): 학습 문제는 주어진 관측값 시퀀스를 사용하여 HMM의 파라미터(상태 전이 확률, 방출 확률, 초기 상태 확률)를 추정하는 문제입니다. Baum-Welch 알고리즘(Expectation-Maximization 알고리즘의 한 종류)은 이 문제를 반복적인 방법으로 해결합니다. 예를 들어, 여러 날 동안의 아이스크림 소비량 데이터를 사용하여 날씨 변화 패턴과 날씨에 따른 아이스크림 소비량 패턴을 학습하는 것입니다.<br>

```python
import numpy as np
from hmmlearn import hmm

# HMM 모델 생성 (초기 파라미터는 랜덤으로 설정됨)
n_states = 2
n_observations = 3
model = hmm.MultinomialHMM(n_components=n_states, n_iter=100)  # n_iter는 학습 반복 횟수

# 학습 데이터 (관측값 시퀀스)
X = np.array([[0], [1], [2], [1], [0], [2], [0], [0]]) # 아이스크림 소비량 시퀀스

# 모델 학습 (Baum-Welch 알고리즘 사용)
model.fit(X)

# 학습된 파라미터 출력
print("학습된 상태 전이 확률:\n", model.transmat_)
print("학습된 방출 확률:\n", model.emissionprob_)
print("학습된 초기 상태 확률:\n", model.startprob_)

# 여러 시퀀스를 사용하여 학습
X_multi = np.array([[0, 1, 2], [2, 1, 0], [0, 0, 1]]).reshape(-1, 1)
lengths = [3, 3, 3]
model_multi = hmm.MultinomialHMM(n_components=n_states, n_iter=100)
model_multi.fit(X_multi, lengths=lengths)
print("\n여러 시퀀스로 학습된 상태 전이 확률:\n", model_multi.transmat_)
print("여러 시퀀스로 학습된 방출 확률:\n", model_multi.emissionprob_)
print("여러 시퀀스로 학습된 초기 상태 확률:\n", model_multi.startprob_)
```
<br><br>

### 은닉 마르코프 모델(Hidden Markov Model)의 활용 분야
---
HMM은 시간적인 맥락을 가지는 데이터를 분석하는 데 매우 유용하며, 다양한 분야에서 활용됩니다.

* 음성 인식: 음성 신호를 분석하여 단어나 문장을 인식합니다. 음성 신호의 변화 패턴을 HMM으로 모델링하여, 발화된 단어를 인식할 수 있습니다.
* 자연어 처리: 텍스트의 품사 태깅, 개체명 인식 등에 사용됩니다. 단어 시퀀스를 관측값으로, 품사 시퀀스를 은닉 상태로 간주하여 문맥에 맞는 품사를 추론할 수 있습니다.
* 생물 정보학: DNA 서열 분석, 단백질 구조 예측 등에 활용됩니다. DNA 염기 서열을 관측값으로, 유전자 또는 단백질의 상태를 은닉 상태로 모델링할 수 있습니다.
* 금융: 주가 예측, 시장 변동성 분석 등에 사용됩니다. 주가 변동을 관측값으로, 시장의 상태를 은닉 상태로 모델링하여 미래의 주가 변동을 예측할 수 있습니다.
* 행동 인식: 비디오에서 사람의 행동을 인식합니다. 비디오 프레임의 변화를 관측값으로, 사람의 행동 패턴을 은닉 상태로 모델링할 수 있습니다.
* 기타: 날씨 예측, 로봇 공학, 제조 공정 모니터링 등 다양한 분야에서 활용됩니다.

<br><br> 

## 예시
---
아래 코드는 HMM의 세 가지 기본 문제(평가, 디코딩, 학습)를 모두 포함하는 예시입니다.
<br>

```python
import numpy as np
from hmmlearn import hmm

# HMM 파라미터 설정
n_states = 2  # 상태 개수
n_observations = 3  # 관측값 개수

start_prob = np.array([0.6, 0.4])  # 초기 상태 확률
trans_mat = np.array([[0.7, 0.3], [0.4, 0.6]])  # 상태 전이 확률
emission_prob = np.array([[0.1, 0.4, 0.5], [0.6, 0.3, 0.1]])  # 방출 확률

# HMM 모델 생성
model = hmm.MultinomialHMM(n_components=n_states, n_iter=100)
model.startprob_ = start_prob
model.transmat_ = trans_mat
model.emissionprob_ = emission_prob

# 관측값 시퀀스
X = np.array([[0], [1], [2], [1], [0]])

# 1. 평가 (Evaluation)
logprob = model.score(X)
probability = np.exp(logprob)
print(f"관측값 시퀀스 발생 확률: {probability}") # 출력 예시: 0.0084672

# 2. 디코딩 (Decoding)
logprob, states = model.decode(X)
print(f"가장 가능성 높은 은닉 상태 시퀀스: {states}") # 출력 예시: [1 1 0 1 1]
print(f"최대 로그 확률: {logprob}") # 출력 예시: -4.770685250328902

# 3. 학습 (Learning) - 새로운 관측값 시퀀스로 학습
X_new = np.array([[1], [0], [2], [2], [0]])
model.fit(X_new)
print("\n학습 후 상태 전이 확률:\n", model.transmat_)
print("학습 후 방출 확률:\n", model.emissionprob_)
print("학습 후 초기 상태 확률:\n", model.startprob_)

# 모델에서 샘플 생성
X_sampled, Z = model.sample(10)  # 10개의 시간 스텝에 대한 샘플 생성
print(f"샘플된 관측값 시퀀스:\n {X_sampled.flatten()}")
print(f"샘플된 은닉 상태 시퀀스:\n {Z}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}