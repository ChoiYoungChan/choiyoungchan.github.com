---
title: "[Python] 파이썬 조건문 if, elif, else 완벽 가이드: 프로그램 흐름 제어의 핵심, 초보자도 쉽게 이해하는 방법"
excerpt: if, elif, else

categories:
  - python
tags:
  - [Python, if, elif, else, 조건문, 파이썬]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

# 파이썬 조건문 if, elif, else 완벽 가이드: 프로그램 흐름 제어의 핵심, 초보자도 쉽게 이해하는 방법

파이썬의 `if`, `elif`, `else`는 조건문으로, 프로그램의 흐름을 제어하는 데 사용됩니다. 특정 조건이 참(True)인지 거짓(False)인지에 따라 실행되는 코드를 결정하여 다양한 상황에 유연하게 대처할 수 있도록 도와줍니다. 이 글에서는 `if`, `elif`, `else` 조건문의 개념, 사용법, 다양한 활용법을 예제 코드와 함께 자세히 설명합니다.

## 1. if 문: 기본 조건 판단

`if` 문은 가장 기본적인 조건문으로, 주어진 조건이 참(True)일 때 특정 코드를 실행합니다.

```python
score = 80

if score >= 60:
    print("합격입니다.")
```

위 예제에서 `score`가 60 이상이면 "합격입니다."가 출력됩니다.

## 2. else 문: if 조건이 거짓일 때 실행

`else` 문은 `if` 문의 조건이 거짓(False)일 때 실행되는 코드를 정의합니다.

```python
score = 40

if score >= 60:
    print("합격입니다.")
else:
    print("불합격입니다.")
```

위 예제에서 `score`가 60 미만이므로 "불합격입니다."가 출력됩니다.

## 3. elif 문: 여러 조건 판단

`elif` 문은 여러 개의 조건을 순차적으로 판단해야 할 때 사용됩니다. `elif`는 "else if"의 줄임말로, 앞선 `if` 또는 `elif` 조건이 거짓일 때 다음 조건을 검사합니다.

```python
score = 75

if score >= 90:
    print("A학점")
elif score >= 80:
    print("B학점")
elif score >= 70:
    print("C학점")
else:
    print("D학점")
```

위 예제에서 `score`가 70 이상 80 미만이므로 "C학점"이 출력됩니다.

## 4. if, elif, else 문 활용 예시

### 4.1. 홀수/짝수 판별

```python
num = int(input("정수를 입력하세요: "))

if num % 2 == 0:
    print("짝수입니다.")
else:
    print("홀수입니다.")
```

### 4.2. 온도에 따른 메시지 출력

```python
temperature = float(input("온도를 입력하세요: "))

if temperature >= 30:
    print("너무 더워요!")
elif temperature >= 20:
    print("적당한 날씨네요.")
else:
    print("조금 춥네요.")
```

### 4.3. 로그인 프로그램

```python
username = input("사용자 이름을 입력하세요: ")
password = input("비밀번호를 입력하세요: ")

if username == "admin" and password == "1234":
    print("로그인 성공!")
elif username == "admin":
    print("비밀번호가 틀렸습니다.")
else:
    print("등록되지 않은 사용자입니다.")
```

## 5. 주의사항

* `if`, `elif`, `else` 문은 들여쓰기를 사용하여 코드 블록을 구분합니다. 들여쓰기가 잘못되면 오류가 발생할 수 있습니다.
* `elif` 문은 `if` 문 뒤에만 사용할 수 있으며, `else` 문은 마지막에 한 번만 사용할 수 있습니다.
* 조건식은 참(True) 또는 거짓(False)을 반환하는 표현식이어야 합니다.

## 6. 결론

`if`, `elif`, `else` 조건문은 프로그램의 흐름을 제어하는 데 필수적인 요소입니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}