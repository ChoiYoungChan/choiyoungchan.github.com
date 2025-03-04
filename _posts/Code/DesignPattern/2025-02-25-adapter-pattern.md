---
title: "[Design Pattern] 어댑터 패턴(Adapter Pattern)의 기본 개념 정리 (C++ 샘플코드 포함)"
excerpt: Adapter Pattern

categories:
  - Design Pattern
tags:
  - [Design Pattern, Adapter, Adapter Pattern, 어댑터 패턴, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2025-02-25
last_modified_at: 2025-02-25
---

## 어댑터 패턴(Adapter Pattern)이란?
---
소프트웨어 개발에서 종종 기존 시스템과 새로운 시스템을 결합해야 하는 경우가 발생합니다. 하지만 두 시스템이 서로 다른 인터페이스를 가지고 있다면 직접 연결할 수 없습니다.

어댑터 패턴은 서로 다른 인터페이스를 가진 클래스들을 호환되도록 변환하는 디자인 패턴인데, 이러한 문제를 해결하기 위해 **중간 변환기** 역할을 하는 클래스를 만들어, 서로 다른 인터페이스를 변환하여 호환성을 보장합니다.
<br><br>

### 사용하는 이유
---
* 기존 코드 수정 없이 새로운 기능을 통합 가능
* 코드 재사용성 증가
* 레거시 시스템과의 호환성 유지
* 의존성 감소로 유지보수 용이
<br><br>

### 어댑터 패턴(Adapter Pattern)의 구성 요소
---
* 클라이언트(Client)
  * 변환된 인터페이스를 사용하는 코드 (예: ```Target```인터페이스를 사용하는 클래스)

* 타겟(Target) 인터페이스
  * 클라이언트가 기대하는 인터페이스
  * 어댑터는 이 인터페이스를 구현해야 함

* 어댑터(Adapter)
  * ```Adaptee```(적응 대상)의 인터페이스를 ```Target```인터페이스로 변환하는 역할

* 적응 대상(Adaptee)
  * 기존 시스템이나 외부 라이브러리 등의 클래스 (호환되지 않는 인터페이스를 가짐)

<br><br>

### 어댑터 패턴(Adapter Pattern)의 장단점
---
#### 장점
✅ 유연성 증가: 기존 시스템을 변경하지 않고 새 인터페이스를 추가할 수 있음<br>
✅ 재사용성 증가: 기존 클래스를 변경 없이 다른 시스템에서 사용할 수 있음<br>
✅ 유지보수성 향상: 코드 수정 없이 새로운 인터페이스와의 호환성을 제공<br>

#### 단점
❌ 구현 복잡성 증가: 변환 계층이 추가되므로 구조가 다소 복잡해질 수 있음<br>
❌ 성능 오버헤드: 어댑터를 거쳐야 하므로 직접 호출보다 성능이 약간 저하될 가능성이 있음
<br><br>

### 활용 예시
---
* 레거시 시스템 통합
  * 오래된 코드(Adaptee)를 새 인터페이스(Target)와 연결할 때 사용
    * 예: 오래된 데이터베이스 API를 새로운 ORM(Object-Relational Mapping) 시스템과 연결

* 외부 라이브러리 사용
  * 외부에서 가져온 라이브러리가 기존 코드와 호환되지 않을 때 어댑터를 활용
    * 예: 외부 결제 API(PayPal, Stripe 등)를 내부 결제 시스템과 연결

* 하드웨어 및 드라이버 개발
  * 서로 다른 운영체제나 장치 간의 인터페이스를 맞추기 위해 사용
    * 예: Windows/Linux에서 서로 다른 네트워크 인터페이스를 맞출 때
<br><br>

## 예시코드
---

[Target 인터페이스 정의]
```C++
#include <iostream>

// 클라이언트가 기대하는 인터페이스
class Target {
public:
    virtual void Request() const {
        std::cout << "Target: 기본 요청 처리\n";
    }
    virtual ~Target() = default;
};
```
<br>

[Adaptee (적응 대상) 정의]
```C++
// 기존 시스템 또는 외부 라이브러리 (호환되지 않는 인터페이스)
class Adaptee {
public:
    void SpecificRequest() const {
        std::cout << "Adaptee: 기존 시스템의 요청 처리\n";
    }
};
```
<br>

[Adapter 구현]
```C++
// Adapter: Adaptee의 인터페이스를 Target 인터페이스로 변환
class Adapter : public Target {
private:
    Adaptee* adaptee;
public:
    Adapter(Adaptee* a) : adaptee(a) {}

    void Request() const override {
        std::cout << "Adapter 변환 중... ";
        adaptee->SpecificRequest();
    }
};
```
<br>

[사용 코드]
```C++
int main() {
    // 기존 시스템 (Adaptee)
    Adaptee* oldSystem = new Adaptee();

    // 어댑터를 통해 기존 시스템을 새 인터페이스(Target)로 변환
    Target* adapter = new Adapter(oldSystem);

    // 클라이언트는 변환된 인터페이스를 사용하여 Adaptee와 통신
    adapter->Request();

    delete oldSystem;
    delete adapter;

    return 0;
}
```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}