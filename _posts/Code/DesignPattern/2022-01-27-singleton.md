---
title: "[Design Pattern] 싱글톤 패턴(Singleton Pattern)의 기본 개념 정리 (C++ 샘플코드 포함)"
excerpt: Singleton Pattern이란

categories:
  - Design Pattern
tags:
  - [Design Pattern, Singleton, Singleton Pattern, 싱글톤 패턴]

toc: true
toc_sticky: true
 
date: 2022-01-27
last_modified_at: 2022-01-27
---

## 싱글톤 패턴(Singleton Pattern)이란?
---
싱글톤 패턴은 클래스의 인스턴스가 단 하나만 생성되는 것을 보장하고, 이 인스턴스에 전역적인 접근 지점을 제공하는 패턴입니다. 즉, 어디에서든 동일한 인스턴스에 접근할 수 있도록 하는 것이 핵심입니다. 마치 회사의 CEO가 한 명인 것처럼, 시스템 전체에서 하나의 객체만 필요한 경우에 유용하게 사용됩니다.<br>


## 사용하는 이유
---
싱글톤 패턴을 사용하는 이유는 여러 가지가 있지만, 주로 다음과 같은 상황에서 유용합니다.

* 하나의 인스턴스만 필요한 경우: 시스템 설정, 데이터베이스 연결, 로깅 관리자 등 시스템 전반에서 하나의 객체만 공유해야 하는 경우가 있습니다. 이 경우 싱글톤 패턴을 사용하면 메모리 낭비를 방지하고 데이터의 일관성을 유지할 수 있습니다. 마치 하나의 수도 계량기로 여러 가구의 물 사용량을 측정하는 것과 같습니다.

* 전역적인 접근이 필요한 경우: 시스템의 여러 부분에서 특정 객체에 접근해야 하는 경우가 있습니다. 싱글톤 패턴을 사용하면 전역 변수를 사용하는 것보다 안전하고 효율적으로 객체에 접근할 수 있습니다. 마치 마을 광장에 있는 시계탑처럼, 마을 어디에서든 시간을 확인할 수 있도록 하는 것과 같습니다.

* 자원 관리의 효율성: 객체 생성 비용이 높은 경우, 여러 번 객체를 생성하는 것은 성능에 영향을 미칠 수 있습니다. 싱글톤 패턴을 사용하면 객체를 한 번만 생성하고 재사용함으로써 자원을 효율적으로 관리할 수 있습니다. 마치 한 번 설치한 다리를 여러 사람이 사용하는 것과 같습니다.
<br><br>

### 장단점
---
#### 장점
* 메모리 절약: 객체를 단 하나만 생성하기 때문에, 동일한 객체를 여러 번 생성할 때 발생하는 메모리 낭비를 줄일 수 있습니다. 마치 하나의 공유 프린터를 여러 사람이 사용하는 것과 같습니다.

* 전역적인 접근 용이: 어디에서든 동일한 인스턴스에 접근할 수 있기 때문에, 전역 변수를 사용하는 것보다 안전하고 편리하게 객체를 공유할 수 있습니다. 마치 마을 중앙에 있는 우체통처럼, 마을 어디에서든 편지를 보낼 수 있는 것과 같습니다.

* 데이터 공유의 효율성: 여러 부분에서 동일한 데이터를 공유해야 할 때, 싱글톤 객체를 통해 데이터를 효율적으로 관리할 수 있습니다. 마치 회사 내의 공지사항 게시판처럼, 모든 직원이 동일한 정보를 확인할 수 있도록 하는 것과 같습니다.


#### 단점
* 과도한 전역 상태: 싱글톤은 전역적인 접근을 제공하기 때문에, 남용할 경우 코드의 결합도를 높이고 유지 보수를 어렵게 만들 수 있습니다. 마치 모든 정보가 하나의 게시판에만 붙어 있는 것처럼, 정보를 찾고 관리하기 어려워지는 것과 같습니다.

* 테스트의 어려움: 싱글톤은 다른 객체들과의 의존성을 숨기기 때문에, 단위 테스트를 어렵게 만들 수 있습니다. 마치 부품이 하나로 붙어 있는 기계처럼, 특정 부품만 테스트하기 어려운 것과 같습니다.

* 멀티 스레드 환경에서의 문제: 여러 스레드가 동시에 싱글톤 객체에 접근할 경우, 동기화 문제가 발생할 수 있습니다. 마치 여러 사람이 동시에 하나의 좁은 문을 통과하려고 하는 것처럼, 혼잡이 발생할 수 있습니다.

* 객체 지향 원칙 위반 가능성: 싱글톤은 객체 지향 프로그래밍의 몇 가지 원칙(예: 단일 책임 원칙)을 위반할 가능성이 있습니다. 마치 하나의 도구가 여러 가지 용도로 사용되는 것처럼, 기능이 분리되지 않아 복잡해질 수 있습니다.

<br>

### 문제점과 해결책
---
* 과도한 전역 상태: 싱글톤의 사용을 최소화하고, 의존성 주입(Dependency Injection)과 같은 다른 디자인 패턴을 활용하여 객체 간의 의존성을 관리하는 것이 좋습니다. 마치 필요한 정보만 관련된 게시판에 나눠 붙이는 것처럼, 정보를 효율적으로 관리할 수 있습니다.

* 테스트의 어려움: 인터페이스를 사용하여 싱글톤 객체를 추상화하고, 테스트 시에는 Mock 객체를 사용하여 테스트를 진행할 수 있습니다. 마치 분리 가능한 부품으로 구성된 기계처럼, 각 부품을 독립적으로 테스트할 수 있습니다.

* 멀티 스레드 환경에서의 문제
  * 정적 변수 초기화: C++11 이상에서는 정적 변수의 초기화가 스레드 안전하게 보장되므로, 앞서 보여드린 예제 코드처럼 static 변수를 사용하여 싱글톤을 구현하면 스레드 안전성을 확보할 수 있습니다.
  * 뮤텍스(Mutex) 사용: 뮤텍스를 사용하여 싱글톤 객체에 대한 접근을 동기화할 수 있습니다. 하지만 과도한 동기화는 성능 저하를 초래할 수 있으므로 주의해야 합니다.

* 객체 지향 원칙 위반 가능성: 싱글톤의 사용을 신중하게 결정하고, 객체 지향 원칙을 준수하는 다른 디자인 패턴을 고려하는 것이 좋습니다.

<br><br>

## 예시 코드
---
싱글톤 패턴을 구현하는 방법은 여러가지가 있으나 기본적으로 Static형 인스턴스를 1개 생성한다는점에서 공통점이 있습니다.
<br> <br> 

[기본형]
```C++
#include <iostream>

class Singleton {
private:
    // 생성자를 private으로 선언하여 외부에서 객체 생성을 막습니다.
    Singleton() {
        std::cout << "Singleton 생성자 호출" << std::endl;
    }

    // 복사 생성자와 복사 할당 연산자를 삭제하여 복제를 막습니다.
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

public:
    // 정적 메서드를 통해 유일한 인스턴스를 반환합니다.
    static Singleton& getInstance() {
        // static 변수를 사용하여 스레드 안전성을 보장합니다 (C++11 이상).
        static Singleton instance;
        return instance;
    }

    void doSomething() {
        std::cout << "Singleton 객체의 doSomething() 메서드 호출" << std::endl;
    }
};

int main() {
    // getInstance() 메서드를 통해 싱글톤 객체에 접근합니다.
    Singleton& instance1 = Singleton::getInstance();
    instance1.doSomething();

    Singleton& instance2 = Singleton::getInstance();
    instance2.doSomething();

    // instance1과 instance2는 동일한 객체를 가리킵니다.
    if (&instance1 == &instance2) {
        std::cout << "instance1과 instance2는 동일한 객체입니다." << std::endl;
    }

    return 0;
}
```

[정적 멤버 변수와 정적 메서드를 사용하는 C++11 이전의 방식]
```C++
#include <iostream>
#include <mutex>

class Singleton {
private:
    Singleton() {
        std::cout << "Singleton 생성자 호출" << std::endl;
    }

    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton* instance;
    static std::mutex mutex; // 뮤텍스 추가

public:
    static Singleton* getInstance() {
        std::lock_guard<std::mutex> lock(mutex); // 뮤텍스 잠금
        if (instance == nullptr) {
            instance = new Singleton();
        }
        return instance;
    }

    void doSomething() {
        std::cout << "Singleton 객체의 doSomething() 메서드 호출" << std::endl;
    }
};

Singleton* Singleton::instance = nullptr; // 정적 멤버 변수 초기화
std::mutex Singleton::mutex; // 뮤텍스 초기화

int main() {
    Singleton* instance1 = Singleton::getInstance();
    instance1->doSomething();

    Singleton* instance2 = Singleton::getInstance();
    instance2->doSomething();

    if (instance1 == instance2) {
        std::cout << "instance1과 instance2는 동일한 객체입니다." << std::endl;
    }

    delete instance1; // 명시적인 해제 필요! (주의!)
    return 0;
}
```
<br>

[Meyers Singleton - 정적 지역 변수를 이용한 방식]
```C++
#include <iostream>

class Singleton {
private:
    // 기본 생성자 (private으로 선언하여 외부에서 직접 생성을 막음)
    Singleton() {
        std::cout << "Singleton 생성자 호출" << std::endl;
    }

    // 복사 생성자 삭제
    Singleton(const Singleton&) = delete;

    // 복사 할당 연산자 삭제
    Singleton& operator=(const Singleton&) = delete;

    // 이동 생성자 삭제 (필요에 따라 구현 가능)
    Singleton(Singleton&&) = delete;

    // 이동 할당 연산자 삭제 (필요에 따라 구현 가능)
    Singleton& operator=(Singleton&&) = delete;

public:
    // 유일한 인스턴스를 반환하는 정적 메서드
    static Singleton& getInstance() {
        static Singleton instance; // 정적 지역 변수. 이 부분이 핵심!
        return instance;
    }

    void doSomething() {
        std::cout << "Singleton 객체의 doSomething() 메서드 호출" << std::endl;
    }

    // 필요에 따라 소멸자를 private으로 선언할 수 있지만,
    // 대부분의 경우 기본 소멸자로 충분합니다.
    ~Singleton() {
        std::cout << "Singleton 소멸자 호출" << std::endl;
    }
};

int main() {
    // getInstance()를 통해 싱글톤 객체에 접근
    Singleton& instance1 = Singleton::getInstance();
    instance1.doSomething();

    Singleton& instance2 = Singleton::getInstance();
    instance2.doSomething();

    // instance1과 instance2는 같은 객체를 가리킴
    if (&instance1 == &instance2) {
        std::cout << "instance1과 instance2는 동일한 객체입니다." << std::endl;
    }

    return 0;
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}