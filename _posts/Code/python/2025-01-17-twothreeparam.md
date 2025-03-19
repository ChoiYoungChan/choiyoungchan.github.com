---
title: "[Python] 파이썬 함수 매개변수 완벽 가이드: 2개, 3개부터 가변 인자까지, 초보자도 쉽게 이해하는 방법"
excerpt: multi param

categories:
  - python
tags:
  - [python, multi param, 매개변수, 파이썬]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

# 파이썬 함수 매개변수 완벽 가이드: 2개, 3개부터 가변 인자까지, 초보자도 쉽게 이해하는 방법

파이썬 함수는 매개변수(parameter)를 통해 외부로부터 데이터를 전달받아 처리할 수 있습니다. 매개변수는 함수의 입력 역할을 하며, 함수의 기능을 다양하게 활용할 수 있도록 도와줍니다. 이 글에서는 파이썬 함수에서 2개, 3개의 매개변수를 사용하는 방법부터 가변 인자, 기본값 매개변수 등 다양한 매개변수 활용법을 예제 코드와 함께 자세히 설명합니다.

## 1. 2개, 3개의 매개변수 사용하기

함수에 2개 또는 3개의 매개변수를 정의하여 다양한 데이터를 전달하고 처리할 수 있습니다.

### 1.1 2개의 매개변수

```python
def add(a, b):
    """두 수를 더하는 함수"""
    return a + b

result = add(5, 3)
print(result)  # 출력: 8
```

### 1.2 3개의 매개변수

```python
def calculate_average(a, b, c):
    """세 수의 평균을 계산하는 함수"""
    return (a + b + c) / 3

average = calculate_average(10, 20, 30)
print(average)  # 출력: 20.0
```

## 2. 가변 인자: 여러 개의 인자 처리하기

가변 인자를 사용하면 함수에 전달되는 인자의 개수를 미리 정하지 않고 여러 개의 인자를 처리할 수 있습니다.

### 2.1 `*args`: 위치 인자 가변 인자

`*args`는 위치 인자 가변 인자를 나타내며, 여러 개의 위치 인자를 튜플 형태로 전달받습니다.

```python
def sum_all(*args):
    """모든 인자의 합을 계산하는 함수"""
    total = 0
    for num in args:
        total += num
    return total

result1 = sum_all(1, 2, 3)
result2 = sum_all(1, 2, 3, 4, 5)
print(result1)  # 출력: 6
print(result2)  # 출력: 15
```

### 2.2 `**kwargs`: 키워드 인자 가변 인자

`**kwargs`는 키워드 인자 가변 인자를 나타내며, 여러 개의 키워드 인자를 딕셔너리 형태로 전달받습니다.

```python
def print_info(**kwargs):
    """키워드 인자 정보를 출력하는 함수"""
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="John", age=30, city="New York")
```

## 3. 기본값 매개변수: 인자 생략 시 기본값 사용

기본값 매개변수를 사용하면 함수 호출 시 인자를 생략했을 때 기본값을 사용할 수 있습니다.

```python
def greet(name, message="안녕하세요!"):
    """인사 메시지를 출력하는 함수"""
    print(f"{name}님, {message}")

greet("Alice")  # 출력: Alice님, 안녕하세요!
greet("Bob", "반갑습니다!")  # 출력: Bob님, 반갑습니다!
```

## 4. 매개변수 활용 시 주의사항

* 함수 호출 시 매개변수의 개수와 순서를 정확히 맞춰야 합니다.
* 가변 인자와 기본값 매개변수를 함께 사용할 때는 순서에 주의해야 합니다.
* 매개변수의 자료형을 명확히 정의하여 오류를 방지하는 것이 좋습니다.

## 5. 결론

파이썬 함수 매개변수는 함수의 기능을 확장하고 다양한 데이터를 처리할 수 있도록 도와줍니다. 2개, 3개의 매개변수부터 가변 인자, 기본값 매개변수까지 다양한 매개변수 활용법을 익히고, 필요에 따라 적절한 매개변수를 선택하여 사용하면 더욱 강력하고 유연한 파이썬 함수를 만들 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}