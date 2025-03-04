---
title: "[Design Pattern] 컴포넌트 패턴(Component Pattern)의 기본 개념 정리 (C++ 샘플코드 포함)"
excerpt: State Pattern

categories:
  - Design Pattern
tags:
  - [Design Pattern, Component, Component Pattern, 컴포넌트 패턴, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2025-02-15
last_modified_at: 2025-02-15
---

## 컴포넌트 패턴(Component Pattern)이란?
---
컴포넌트 패턴은 객체 지향 프로그래밍(OOP)의 전통적인 계층적 상속(Inheritance) 방식 대신, 조합(Composition) 방식을 사용하여 객체를 구성하는 방법인데, 쉽게 말해 소프트웨어 설계에서 개별적인 기능을 독립적인 컴포넌트로 나누어 모듈화하는 패턴입니다 이 패턴은 특히 게임 개발에서 널리 사용되며, Unity, Unreal Engine과 같은 게임 엔진에서도 핵심 아키텍처로 활용됩니다.
<br><br>

### 사용하는 이유
---
* 유연한 설계: 객체 간 결합도를 낮춰 변경이 쉽다.
* 코드 재사용성: 여러 개체에서 동일한 컴포넌트를 공유할 수 있다.
* 확장성: 새로운 기능을 쉽게 추가할 수 있다.
* 단일 책임 원칙(SRP, Single Responsibility Principle) 준수: 하나의 컴포넌트는 특정한 역할만 담당한다.
<br><br>

### 컴포넌트 패턴(Component Pattern)의 구성 요소
---
* 엔티티(Entity)
  * 게임 내에서 개별적인 객체(예: 플레이어, 적, 총알 등)
  * 직접적인 기능을 가지지 않고, 여러 컴포넌트를 보유하여 행동을 결정함

* 컴포넌트(Component)
  * 엔티티가 가지는 독립적인 기능 요소
  * 예를 들어, TransformComponent(위치/회전/크기 정보), PhysicsComponent(물리 연산), RenderComponent(렌더링) 등이 있음
  * 독립적으로 설계되며, 재사용 가능

* 컴포넌트 관리자(Component Manager)
  * 전체 시스템에서 특정 유형의 컴포넌트들을 관리하는 역할
  * 예를 들어, PhysicsSystem은 모든 PhysicsComponent를 업데이트함
<br><br>

### 특징
---
* 객체 조합(Composition over Inheritance) : 전통적인 OOP 상속 대신, 엔티티는 여러 개의 컴포넌트를 포함하여 동작함.
* 유연한 기능 추가 및 제거 : 새로운 기능을 추가하려면 기존 클래스를 변경할 필요 없이, 새로운 컴포넌트를 엔티티에 추가하면 됨.
* 컴포넌트 간 독립성 : 특정 기능(예: 물리 엔진, 애니메이션, 렌더링 등)이 서로 영향을 주지 않음.
<br><br>

### 컴포넌트 패턴(Component Pattern)의 장단점
---
#### 장점
✅유연한 설계:<br>
엔티티가 특정 클래스를 상속할 필요 없이 다양한 기능을 조합할 수 있음.<br><br>
✅ 확장성:<br>
새로운 기능을 추가하려면 컴포넌트를 만들고 엔티티에 추가하면 됨.<br><br>
✅ 재사용성 증가:<br>
같은 RenderComponent를 여러 엔티티에서 사용할 수 있음.<br><br>
✅ 단일 책임 원칙(SRP) 준수:<br>
각 컴포넌트는 특정 역할만 수행하며, 코드가 명확해짐.<br><br>

#### 단점
❌ 관리 비용 증가:<br>
컴포넌트 간 의존성을 잘못 관리하면 복잡도가 증가할 수 있음.<br><br>
❌ 메모리 오버헤드:<br>
객체마다 여러 개의 컴포넌트를 유지해야 하므로 메모리 사용량이 증가할 가능성이 있음.<br><br>
❌ 성능 문제:<br>
런타임에서 동적으로 컴포넌트를 찾고 처리해야 하므로, 잘못된 설계 시 성능 저하 가능.
<br><br>

### 활용 예시
---
* 게임 엔진
  * Unity: GameObject + Component 구조
  * Unreal Engine: Actor + Component 구조

* 소프트웨어 개발
  * UI 시스템: 버튼, 텍스트 필드 등의 GUI 컴포넌트
  * IoT 시스템: 센서, 데이터 처리 모듈을 독립적인 컴포넌트로 설계
<br><br>

## 예시코드
---

[컴포넌트 인터페이스 정의]
```C++
#include <iostream>
#include <vector>
#include <memory>

// 컴포넌트 기본 클래스 (모든 컴포넌트가 상속)
class Component {
public:
    virtual ~Component() = default;
    virtual void Update() = 0; // 각 컴포넌트는 Update 메서드를 가짐
};
```
<br>

[구체적인 컴포넌트 구현]
```C++
// 위치(Transform) 컴포넌트
class TransformComponent : public Component {
public:
    float x, y;

    TransformComponent(float x = 0, float y = 0) : x(x), y(y) {}

    void Update() override {
        std::cout << "Transform 업데이트: (" << x << ", " << y << ")\n";
    }
};

// 물리(Physics) 컴포넌트
class PhysicsComponent : public Component {
public:
    float velocity;

    PhysicsComponent(float velocity = 0) : velocity(velocity) {}

    void Update() override {
        std::cout << "Physics 업데이트: 속도 " << velocity << "\n";
    }
};
```
<br>

[엔티티(Entity) 정의]
```C++
class Entity {
private:
    std::vector<std::shared_ptr<Component>> components;

public:
    void AddComponent(std::shared_ptr<Component> component) {
        components.push_back(component);
    }

    void Update() {
        for (auto& component : components) {
            component->Update();
        }
    }
};
```
<br>

[사용 코드]
```C++
int main() {
    Entity player;

    // 플레이어에 Transform과 Physics 컴포넌트 추가
    player.AddComponent(std::make_shared<TransformComponent>(10, 20));
    player.AddComponent(std::make_shared<PhysicsComponent>(5));

    // 모든 컴포넌트 업데이트
    player.Update();

    return 0;
}
```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}