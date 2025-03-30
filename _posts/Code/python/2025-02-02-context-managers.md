---
title: "[Python] 파이썬 컨텍스트 관리자(Context Managers) 완벽 가이드: 리소스 관리의 핵심, 초보자도 쉽게 이해하는 방법"
excerpt: context managers

categories:
  - python
tags:
  - [Python, context managers, 컨텍스트 관리자, 파이썬]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

# 파이썬 컨텍스트 관리자(Context Managers) 완벽 가이드: 리소스 관리의 핵심, 초보자도 쉽게 이해하는 방법

파이썬 컨텍스트 관리자(Context Managers)는 특정 코드 블록의 실행 전후에 필요한 작업을 자동으로 처리하는 기능을 제공합니다. 컨텍스트 관리자를 사용하면 파일, 네트워크 연결, 스레드 잠금 등 다양한 리소스를 효율적으로 관리하고 코드의 가독성을 높일 수 있습니다. 이 글에서는 파이썬 컨텍스트 관리자의 기본 개념, 사용법, 다양한 활용법을 예제 코드와 함께 자세히 설명합니다.

## 1. 컨텍스트 관리자(Context Managers)란 무엇인가?

컨텍스트 관리자는 `with` 문과 함께 사용되어 코드 블록의 실행 전후에 특정 작업을 자동으로 처리합니다. 예를 들어, 파일을 열고 닫거나, 네트워크 연결을 설정하고 해제하는 등의 작업을 자동으로 처리할 수 있습니다.

## 2. 컨텍스트 관리자 사용법

### 2.1. `with` 문

`with` 문은 컨텍스트 관리자를 사용하여 코드 블록을 실행합니다. `with` 문이 시작될 때 컨텍스트 관리자의 `__enter__` 메서드가 호출되고, 코드 블록이 종료될 때 `__exit__` 메서드가 호출됩니다.

```python
with open("my_file.txt", "w") as f:
    f.write("Hello, World!")
```

### 2.2. 컨텍스트 관리자 클래스

`__enter__`와 `__exit__` 메서드를 구현하여 사용자 정의 컨텍스트 관리자 클래스를 만들 수 있습니다.

```python
class MyContextManager:
    def __enter__(self):
        print("Entering context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting context")

with MyContextManager() as manager:
    print("Inside context")
```

### 2.3. `contextlib` 모듈

`contextlib` 모듈은 컨텍스트 관리자를 쉽게 만들 수 있도록 도와주는 도구를 제공합니다.

* `contextmanager` 데코레이터: 제너레이터 함수를 컨텍스트 관리자로 변환합니다.
* `closing` 함수: `close()` 메서드를 가진 객체를 컨텍스트 관리자로 변환합니다.

```python
from contextlib import contextmanager

@contextmanager
def my_context_manager():
    print("Entering context")
    yield
    print("Exiting context")

with my_context_manager():
    print("Inside context")
```

## 3. 컨텍스트 관리자 활용

### 3.1. 파일 처리

파일을 열고 닫는 작업을 자동으로 처리합니다.

```python
with open("my_file.txt", "r") as f:
    contents = f.read()
    print(contents)
```

### 3.2. 네트워크 연결

네트워크 연결을 설정하고 해제하는 작업을 자동으로 처리합니다.

```python
import socket

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect(("www.example.com", 80))
    # 네트워크 통신 코드
```

### 3.3. 스레드 잠금

스레드 잠금을 설정하고 해제하는 작업을 자동으로 처리합니다.

```python
import threading

lock = threading.Lock()
with lock:
    # 스레드 안전 코드
```

### 3.4. 데이터베이스 연결

데이터베이스 연결을 설정하고 해제하는 작업을 자동으로 처리합니다.

```python
import sqlite3

with sqlite3.connect("my_database.db") as conn:
    cursor = conn.cursor()
    # 데이터베이스 작업 코드
```

## 4. 결론

파이썬 컨텍스트 관리자는 리소스를 효율적으로 관리하고 코드의 가독성을 높이는 데 유용한 도구입니다. `with` 문과 `contextlib` 모듈을 활용하여 더욱 안전하고 효율적인 파이썬 코드를 작성할 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}