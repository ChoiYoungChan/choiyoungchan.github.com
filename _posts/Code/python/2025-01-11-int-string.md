---
title: "[Python] 파이썬 int와 string 완벽 분석: 숫자와 문자의 모든 것, 초보자도 쉽게 이해하는 핵심 가이드"
excerpt: int, string in python

categories:
  - python
tags:
  - [python, string, int, 파이썬]

toc: true
toc_sticky: true
 
date: 2025-01-11
last_modified_at: 2025-01-11
---

# 파이썬 int와 string 완벽 분석: 숫자와 문자의 모든 것, 초보자도 쉽게 이해하는 핵심 가이드

파이썬은 다양한 자료형을 제공하여 효율적인 프로그래밍을 지원합니다. 그중에서도 int(정수)와 string(문자열)은 가장 기본적이면서도 핵심적인 자료형입니다. 이 글에서는 int와 string의 개념, 사용법, 주의사항 등을 자세히 설명하여 초보자도 쉽게 이해하고 활용할 수 있도록 돕겠습니다.

## 1. int(정수): 숫자를 다루는 기본 자료형

### 1.1 int란 무엇인가?

int는 정수(integer)를 표현하는 자료형입니다. 양수, 음수, 0을 포함하는 모든 정수를 나타낼 수 있습니다. 파이썬에서는 정수의 크기에 제한이 없어 매우 큰 숫자도 처리할 수 있습니다.

### 1.2 int 생성 및 기본 연산

```python
# int 생성
a = 10
b = -5
c = 0

# 기본 연산
print(a + b)  # 출력: 5
print(a - b)  # 출력: 15
print(a * b)  # 출력: -50
print(a / b)  # 출력: -2.0 (나눗셈 결과는 float)
print(a // b) # 출력: -2 (정수 나눗셈)
print(a % b)  # 출력: 0 (나머지)
print(a ** 2) # 출력: 100 (제곱)
```

### 1.3 int 관련 유용한 함수

* `abs(x)`: x의 절댓값을 반환합니다.
* `pow(x, y)`: x의 y제곱을 반환합니다.
* `divmod(x, y)`: x를 y로 나눈 몫과 나머지를 튜플 형태로 반환합니다.

```python
a = -10
print(abs(a))  # 출력: 10

print(pow(2, 3))  # 출력: 8

print(divmod(10, 3))  # 출력: (3, 1)
```

### 1.4 int 활용 예시

int는 다양한 상황에서 활용됩니다.

* **수학 계산**: 사칙연산, 제곱, 나머지 등 다양한 수학 계산을 수행합니다.
* **반복문 제어**: `for` 루프, `while` 루프 등 반복문의 횟수를 제어합니다.
* **인덱싱**: 리스트, 튜플 등 순서가 있는 자료형의 요소에 접근할 때 인덱스로 사용됩니다.

```python
# 반복문 예시
for i in range(5):
    print(i)

# 인덱싱 예시
my_list = [10, 20, 30]
print(my_list[0])  # 출력: 10
```

### 1.5 int 사용 시 주의사항

* 나눗셈 연산자(`/`)는 결과를 항상 float로 반환합니다. 정수 나눗셈을 원하면 `//` 연산자를 사용해야 합니다.
* 큰 수를 다룰 때는 메모리 사용량에 주의해야 합니다.

## 2. string(문자열): 문자를 다루는 기본 자료형

### 2.1 string이란 무엇인가?

string은 문자열(string)을 표현하는 자료형입니다. 문자, 숫자, 기호 등을 포함하는 문자들의 순서 있는 집합입니다. 파이썬에서는 작은따옴표(`'`) 또는 큰따옴표(`"`)로 문자열을 생성합니다.

### 2.2 string 생성 및 기본 연산

```python
# string 생성
s1 = 'Hello'
s2 = "World"

# 문자열 연결
print(s1 + s2)  # 출력: HelloWorld

# 문자열 반복
print(s1 * 3)  # 출력: HelloHelloHello

# 문자열 길이
print(len(s1))  # 출력: 5

# 문자열 인덱싱
print(s1[0])  # 출력: H
print(s1[-1]) # 출력: o

# 문자열 슬라이싱
print(s1[1:4]) # 출력: ell
```

### 2.3 string 관련 유용한 메서드

* `upper()`: 문자열을 모두 대문자로 변환합니다.
* `lower()`: 문자열을 모두 소문자로 변환합니다.
* `strip()`: 문자열 양쪽의 공백을 제거합니다.
* `split(sep)`: `sep`을 기준으로 문자열을 분리하여 리스트로 반환합니다.
* `find(sub)`: 문자열에서 `sub`의 위치를 찾아 인덱스를 반환합니다.
* `replace(old, new)`: 문자열에서 `old`를 `new`로 바꿉니다.

```python
s = "  Hello, World!  "
print(s.upper())  # 출력:   HELLO, WORLD!
print(s.strip())  # 출력: Hello, World!
print(s.split(","))  # 출력: ['  Hello', ' World!  ']
print(s.find("World"))  # 출력: 9
print(s.replace("World", "Python")) # 출력: Hello, Python!
```

### 2.4 string 활용 예시

string은 다양한 상황에서 활용됩니다.

* **텍스트 처리**: 문자열 검색, 치환, 분리 등 다양한 텍스트 처리를 수행합니다.
* **사용자 입력 처리**: 사용자로부터 입력받은 문자열을 처리합니다.
* **파일 입출력**: 파일에서 문자열을 읽거나 파일에 문자열을 씁니다.

```python
# 사용자 입력 처리 예시
name = input("이름을 입력하세요: ")
print("안녕하세요, " + name + "님!")

# 파일 입출력 예시
with open("test.txt", "w") as f:
    f.write("Hello, World!")

with open("test.txt", "r") as f:
    content = f.read()
    print(content)
```

### 2.5 string 사용 시 주의사항

* 문자열은 불변(immutable) 자료형이므로, 문자열의 특정 문자를 직접 변경할 수 없습니다.
* 문자열 연결 시에는 새로운 문자열이 생성되므로, 많은 문자열을 연결할 때는 `join()` 메서드를 사용하는 것이 효율적입니다.
* 문자열 포맷팅을 사용하면 문자열을 더욱 깔끔하게 생성할 수 있습니다.

## 3. 결론

파이썬 int와 string은 데이터를 다루는 데 필수적인 자료형입니다. int는 숫자를, string은 문자를 표현하며, 다양한 연산과 메서드를 통해 효율적인 데이터 처리를 지원합니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}