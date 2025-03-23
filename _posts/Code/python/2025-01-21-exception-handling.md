---
title: "[Python] 파이썬 예외 처리(Exception Handling) 완벽 가이드: 안정적인 프로그램 작성을 위한 필수 기술, 초보자도 쉽게 이해하는 방법"
excerpt: Exception Handling

categories:
  - python
tags:
  - [python, Exception Handling, 예외 처리, 파이썬]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

# 파이썬 예외 처리(Exception Handling) 완벽 가이드: 안정적인 프로그램 작성을 위한 필수 기술, 초보자도 쉽게 이해하는 방법

파이썬 예외 처리(Exception Handling)는 프로그램 실행 중에 발생할 수 있는 오류(예외)를 처리하여 프로그램이 갑작스럽게 종료되는 것을 방지하고, 안정적으로 실행될 수 있도록 하는 기술입니다. 예외 처리를 통해 예상치 못한 상황에서도 프로그램이 정상적으로 작동하도록 만들 수 있습니다. 이 글에서는 파이썬 예외 처리의 개념, 사용법, 다양한 활용법을 예제 코드와 함께 자세히 설명합니다.

## 1. 예외(Exception)란 무엇인가?

예외는 프로그램 실행 중에 발생하는 오류를 의미합니다. 예를 들어, 존재하지 않는 파일을 열려고 하거나, 0으로 숫자를 나누는 경우 예외가 발생합니다. 예외가 발생하면 프로그램은 해당 지점에서 중단되고 오류 메시지를 출력합니다.

## 2. 예외 처리 기본 문법: try, except

`try` 블록에는 예외가 발생할 가능성이 있는 코드를 작성하고, `except` 블록에는 예외가 발생했을 때 실행할 코드를 작성합니다.

```python
try:
    # 예외 발생 가능성이 있는 코드
    result = 10 / 0
except ZeroDivisionError:
    # 예외 처리 코드
    print("0으로 나눌 수 없습니다.")
```

위 예제에서 `10 / 0`은 `ZeroDivisionError` 예외를 발생시키므로, `except` 블록의 코드가 실행되어 "0으로 나눌 수 없습니다."가 출력됩니다.

## 3. 다양한 예외 처리

### 3.1. 여러 개의 except 블록

하나의 `try` 블록에 여러 개의 `except` 블록을 사용하여 다양한 예외를 처리할 수 있습니다.

```python
try:
    num = int(input("숫자를 입력하세요: "))
    result = 10 / num
    print(result)
except ValueError:
    print("잘못된 입력입니다. 숫자를 입력하세요.")
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
```

### 3.2. 모든 예외 처리: except Exception

`except Exception`을 사용하여 모든 예외를 처리할 수 있습니다. 하지만 특정 예외에 대한 처리가 필요하다면 구체적인 예외를 명시하는 것이 좋습니다.

```python
try:
    # 예외 발생 가능성이 있는 코드
    ...
except Exception as e:
    print(f"예외 발생: {e}")
```

### 3.3. else 블록

`else` 블록은 `try` 블록에서 예외가 발생하지 않았을 때 실행됩니다.

```python
try:
    num = int(input("숫자를 입력하세요: "))
    result = 10 / num
except ValueError:
    print("잘못된 입력입니다. 숫자를 입력하세요.")
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
else:
    print(f"결과: {result}")
```

### 3.4. finally 블록

`finally` 블록은 예외 발생 여부와 상관없이 항상 실행됩니다. 파일 닫기, 네트워크 연결 종료 등 자원 해제에 사용됩니다.

```python
try:
    f = open("test.txt", "r")
    data = f.read()
    print(data)
except FileNotFoundError:
    print("파일을 찾을 수 없습니다.")
finally:
    if 'f' in locals():
        f.close()
```

## 4. 사용자 정의 예외

`Exception` 클래스를 상속받아 사용자 정의 예외를 만들 수 있습니다.

```python
class MyError(Exception):
    def __init__(self, message):
        self.message = message

try:
    raise MyError("사용자 정의 예외 발생")
except MyError as e:
    print(f"사용자 정의 예외: {e.message}")
```

## 5. 예외 처리 활용 예시

### 5.1. 파일 입출력 오류 처리

```python
try:
    f = open("data.txt", "r")
    # 파일 처리 코드
except FileNotFoundError:
    print("파일을 찾을 수 없습니다.")
except IOError:
    print("파일 입출력 오류 발생")
```

### 5.2. 네트워크 통신 오류 처리

```python
import requests

try:
    response = requests.get("https://www.example.com")
    response.raise_for_status()  # HTTP 오류 발생 시 예외 발생
except requests.exceptions.RequestException as e:
    print(f"네트워크 오류: {e}")
```

## 6. 결론

파이썬 예외 처리는 안정적인 프로그램 작성을 위한 필수 기술입니다. `try`, `except`, `else`, `finally` 블록과 사용자 정의 예외를 활용하여 다양한 예외 상황에 대처하고, 견고한 파이썬 프로그램을 개발할 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}