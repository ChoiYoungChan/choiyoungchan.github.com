---
title: "[Python] 파이썬 입력(Input)과 출력(Output) 완벽 가이드: 사용자 상호작용의 핵심, 초보자도 쉽게 이해하는 방법"
excerpt: Input, Output

categories:
  - python
tags:
  - [Python, Output, Input, 입력, 출력]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

# 파이썬 입력(Input)과 출력(Output) 완벽 가이드: 사용자 상호작용의 핵심, 초보자도 쉽게 이해하는 방법

파이썬은 사용자로부터 데이터를 입력받고 결과를 출력하는 기능을 제공하여 프로그램과 사용자 간의 상호작용을 가능하게 합니다. 입력(Input)과 출력(Output)은 프로그래밍의 기본적인 요소이며, 사용자 친화적인 프로그램을 만드는 데 필수적입니다. 이 글에서는 파이썬의 입력과 출력에 대한 개념, 사용법, 다양한 활용법을 예제 코드와 함께 자세히 설명합니다.

## 1. 입력(Input): 사용자로부터 데이터 받기

### 1.1 input() 함수

`input()` 함수는 사용자로부터 문자열을 입력받는 데 사용됩니다. 사용자가 키보드로 입력한 내용은 문자열 형태로 반환됩니다.

```python
name = input("이름을 입력하세요: ")
print("안녕하세요, " + name + "님!")
```

### 1.2 입력받은 데이터 타입 변환

`input()` 함수는 항상 문자열을 반환하므로, 숫자나 다른 타입의 데이터를 입력받으려면 타입 변환이 필요합니다.

```python
age = int(input("나이를 입력하세요: "))
print("내년에는 " + str(age + 1) + "살이 됩니다.")
```

### 1.3 여러 개의 입력 받기

`split()` 메서드를 사용하여 여러 개의 입력을 한 번에 받을 수 있습니다.

```python
a, b = input("두 개의 숫자를 공백으로 구분하여 입력하세요: ").split()
a = int(a)
b = int(b)
print("두 수의 합:", a + b)
```

## 2. 출력(Output): 결과를 화면에 표시하기

### 2.1 print() 함수

`print()` 함수는 화면에 데이터를 출력하는 데 사용됩니다. 여러 개의 인자를 쉼표(`,`)로 구분하여 전달할 수 있습니다.

```python
print("Hello, World!")
print("이름:", name, "나이:", age)
```

### 2.2 문자열 포맷팅

문자열 포맷팅을 사용하면 변수의 값을 문자열 안에 삽입하여 깔끔하게 출력할 수 있습니다.

* **f-string**: 파이썬 3.6부터 지원하는 문자열 포맷팅 방식입니다.

```python
print(f"이름: {name}, 나이: {age}")
```

* **format() 메서드**: 문자열의 `format()` 메서드를 사용하여 변수의 값을 삽입할 수 있습니다.

```python
print("이름: {}, 나이: {}".format(name, age))
```

### 2.3 파일 출력

`print()` 함수를 사용하여 파일에 데이터를 출력할 수도 있습니다.

```python
with open("output.txt", "w") as f:
    print("Hello, File!", file=f)
```

## 3. 입력과 출력 활용 예시

### 3.1 계산기 프로그램

```python
num1 = float(input("첫 번째 숫자를 입력하세요: "))
operator = input("연산자를 입력하세요 (+, -, *, /): ")
num2 = float(input("두 번째 숫자를 입력하세요: "))

if operator == "+":
    result = num1 + num2
elif operator == "-":
    result = num1 - num2
elif operator == "*":
    result = num1 * num2
elif operator == "/":
    result = num1 / num2
else:
    print("잘못된 연산자입니다.")
    result = None

if result is not None:
    print("결과:", result)
```

### 3.2 사용자 정보 입력 및 출력

```python
name = input("이름을 입력하세요: ")
age = int(input("나이를 입력하세요: "))
city = input("사는 도시를 입력하세요: ")

print(f"사용자 정보: 이름={name}, 나이={age}, 도시={city}")
```

## 4. 결론

파이썬의 입력과 출력은 사용자 상호작용을 가능하게 하는 핵심 기능입니다. `input()` 함수를 사용하여 사용자로부터 데이터를 입력받고, `print()` 함수를 사용하여 결과를 화면이나 파일에 출력할 수 있습니다. 문자열 포맷팅을 사용하면 더욱 깔끔하고 가독성 높은 출력을 만들 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}