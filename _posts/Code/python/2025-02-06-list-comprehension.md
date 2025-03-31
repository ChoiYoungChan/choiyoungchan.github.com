---
title: "[Python] 파이썬 리스트 컴프리헨션(List Comprehension) 완벽 가이드: 간결하고 효율적인 리스트 생성의 핵심, 초보자부터 전문가까지"
excerpt: List Comprehension

categories:
  - python
tags:
  - [Python, List Comprehension, 리스트 컴프리헨션, 파이썬]

toc: true
toc_sticky: true
 
date: 2025-02-06
last_modified_at: 2025-02-06
---

# 파이썬 리스트 컴프리헨션(List Comprehension) 완벽 가이드: 간결하고 효율적인 리스트 생성의 핵심, 초보자부터 전문가까지

파이썬 리스트 컴프리헨션(List Comprehension)은 반복문과 조건문을 사용하여 간결하고 효율적으로 리스트를 생성하는 강력한 기능입니다. 리스트 컴프리헨션을 사용하면 코드의 가독성을 높이고 실행 속도를 향상시킬 수 있습니다. 이 글에서는 파이썬 리스트 컴프리헨션의 기본 개념, 다양한 활용법, 성능 최적화 방법 등을 예제 코드와 함께 자세히 설명합니다.

## 1. 리스트 컴프리헨션(List Comprehension)이란 무엇인가?

리스트 컴프리헨션은 다음과 같은 기능을 수행합니다.

* 반복문(for loop)과 조건문(if statement)을 사용하여 리스트를 생성합니다.
* 간결하고 가독성이 높은 코드를 작성할 수 있습니다.
* 실행 속도가 빠릅니다.

## 2. 리스트 컴프리헨션 기본 문법

리스트 컴프리헨션의 기본 문법은 다음과 같습니다.

```python
[expression for item in iterable if condition]
```

* `expression`: 각 요소에 적용할 표현식입니다.
* `item`: 반복 가능한 객체(iterable)의 각 요소입니다.
* `iterable`: 반복 가능한 객체(리스트, 튜플, 문자열 등)입니다.
* `condition`: 각 요소를 필터링하는 조건식입니다. (선택 사항)

## 3. 리스트 컴프리헨션 사용 예시

### 3.1. 리스트의 각 요소에 제곱 연산 적용

```python
numbers = [1, 2, 3, 4, 5]
squared_numbers = [x ** 2 for x in numbers]
print(squared_numbers)  # 출력: [1, 4, 9, 16, 25]
```

### 3.2. 짝수만 추출하여 리스트 생성

```python
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = [x for x in numbers if x % 2 == 0]
print(even_numbers)  # 출력: [2, 4, 6]
```

### 3.3. 문자열 리스트를 대문자로 변환

```python
words = ["apple", "banana", "cherry"]
upper_words = [word.upper() for word in words]
print(upper_words)  # 출력: ['APPLE', 'BANANA', 'CHERRY']
```

### 3.4. 중첩 리스트 컴프리헨션

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened_matrix = [num for row in matrix for num in row]
print(flattened_matrix)  # 출력: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 4. 다양한 리스트 컴프리헨션 활용

### 4.1. 조건부 표현식 사용

```python
numbers = [1, 2, 3, 4, 5]
result = ["짝수" if x % 2 == 0 else "홀수" for x in numbers]
print(result)  # 출력: ['홀수', '짝수', '홀수', '짝수', '홀수']
```

### 4.2. 딕셔너리 컴프리헨션

딕셔너리 컴프리헨션을 사용하여 딕셔너리를 생성할 수 있습니다.

```python
numbers = [1, 2, 3, 4, 5]
squared_dict = {x: x ** 2 for x in numbers}
print(squared_dict)  # 출력: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

### 4.3. 집합 컴프리헨션

집합 컴프리헨션을 사용하여 집합을 생성할 수 있습니다.

```python
numbers = [1, 2, 2, 3, 3, 3]
unique_numbers = {x for x in numbers}
print(unique_numbers)  # 출력: {1, 2, 3}
```

### 4.4. 제너레이터 표현식

제너레이터 표현식은 리스트 컴프리헨션과 유사하지만, 리스트 대신 제너레이터를 생성합니다. 제너레이터는 메모리 사용량을 줄이는 데 유용합니다.

```python
numbers = [1, 2, 3, 4, 5]
squared_generator = (x ** 2 for x in numbers)
print(squared_generator)  # 출력: <generator object <genexpr> at 0x...>

for num in squared_generator:
    print(num)  # 출력: 1, 4, 9, 16, 25
```

## 5. 리스트 컴프리헨션 성능 최적화

### 5.1. 반복문 대신 리스트 컴프리헨션 사용

리스트 컴프리헨션은 반복문보다 실행 속도가 빠릅니다.

```python
# 느린 코드
result = []
for x in range(1000000):
    result.append(x ** 2)

# 빠른 코드
result = [x ** 2 for x in range(1000000)]
```

### 5.2. 불필요한 연산 제거

리스트 컴프리헨션 내부에서 불필요한 연산을 제거하여 성능을 향상시킬 수 있습니다.

### 5.3. 제너레이터 표현식 활용

메모리 사용량이 많은 경우 제너레이터 표현식을 사용하여 성능을 향상시킬 수 있습니다.

## 6. 리스트 컴프리헨션 주의사항

### 6.1. 가독성 유지

너무 복잡한 리스트 컴프리헨션은 가독성을 떨어뜨릴 수 있습니다. 적절한 수준에서 사용하는 것이 좋습니다.

### 6.2. 메모리 사용량 고려

큰 데이터셋을 처리할 때는 메모리 사용량을 고려해야 합니다. 제너레이터 표현식을 사용하여 메모리 사용량을 줄일 수 있습니다.

## 7. 결론

파이썬 리스트 컴프리헨션은 간결하고 효율적인 리스트 생성의 핵심 기능입니다. 다양한 활용법과 성능 최적화 방법을 익히고, 필요에 따라 적절한 방법을 선택하여 사용하면 더욱 효율적인 파이썬 코드를 작성할 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}