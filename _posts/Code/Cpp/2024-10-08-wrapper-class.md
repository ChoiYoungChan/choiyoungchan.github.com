---
title:  "[C++] Wrapper Class"
excerpt: Wrapper Class in C++

categories:
  - Cpp
tags:
  - [Programming, c++, Wrapper, Cpp]

toc: true
toc_sticky: true
 
date: 2024-10-08
last_modified_at: 2024-10-08
---

## Wrapper의 개념
---
Wrapper 클래스는 원시 데이터 타입 또는 기존 클래스를 감싸(encapsulate)서 더 높은 수준의 추상화를 제공하거나 특정 기능을 확장하기 위한 클래스입니다. 일반적으로 다음과 같은 목적으로 사용됩니다
<br><br>

### Wrapper 클래스의 주요 목적과 사용처
---

* 추상화
  * 기본 데이터 타입이나 복잡한 데이터를 더 쉽게 다룰 수 있도록 인터페이스를 제공합니다.

* 기능 확장
  * 기존 데이터나 클래스에 새로운 기능을 추가하거나, 특정 제한을 두는 역할을 수행합니다.

* 메모리 관리
  * 동적 메모리 할당/해제를 관리하거나 스마트 포인터처럼 자원 관리 역할을 수행합니다.

* 유효성 검사
  * 데이터를 안전하게 다루기 위해 유효성 검사를 수행합니다.

* 호환성
  * 레거시 코드나 특정 API와의 통합을 위해 데이터를 적절히 변환하거나 처리합니다.
<br><br>

### 특징
---
* 은닉성: 내부 데이터를 외부로부터 숨기고, 메서드를 통해 데이터에 접근하도록 설계합니다.
* 확장 가능성: 기존 데이터 타입에 새로운 연산자 오버로딩, 기능 등을 추가할 수 있습니다.
* 유연성: 다양한 데이터 타입을 다룰 수 있도록 템플릿을 사용한 Wrapper 클래스를 작성할 수 있습니다.
<br><br>


## 코드 및 설명
---

```c++
#include <iostream>
#include <stdexcept>

// Wrapper 클래스 정의
class IntWrapper {
private:
    int value; // 감싸는 기본 데이터 타입

public:
    // 생성자
    IntWrapper(int val = 0) : value(val) {}

    // 값을 설정하는 함수 (유효성 검사 포함)
    void setValue(int val) {
        if (val < 0) {
            throw std::invalid_argument("Value cannot be negative!");
        }
        value = val;
    }

    // 값을 가져오는 함수
    int getValue() const {
        return value;
    }

    // 연산자 오버로딩: 덧셈
    IntWrapper operator+(const IntWrapper& other) const {
        return IntWrapper(value + other.value);
    }

    // 연산자 오버로딩: 출력 (<<)
    friend std::ostream& operator<<(std::ostream& os, const IntWrapper& obj) {
        os << obj.value;
        return os;
    }

    // 연산자 오버로딩: 입력 (>>)
    friend std::istream& operator>>(std::istream& is, IntWrapper& obj) {
        is >> obj.value;
        if (obj.value < 0) {
            throw std::invalid_argument("Value cannot be negative!");
        }
        return is;
    }
};

// 사용 예제
int main() {
    try {
        IntWrapper a(10);  // 초기화
        IntWrapper b;      // 기본값 0
        b.setValue(20);    // 값 설정

        // 덧셈 연산
        IntWrapper c = a + b;

        // 결과 출력
        std::cout << "a: " << a << ", b: " << b << ", c: " << c << std::endl;

        // 사용자로부터 입력받기
        IntWrapper d;
        std::cout << "Enter a value for d: ";
        std::cin >> d;
        std::cout << "d: " << d << std::endl;

    } catch (const std::exception& ex) {
        std::cerr << "Error: " << ex.what() << std::endl;
    }

    return 0;
}
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}

