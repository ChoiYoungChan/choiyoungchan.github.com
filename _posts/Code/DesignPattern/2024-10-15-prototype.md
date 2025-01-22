---
title: "[Design Pattern] 프로토타입 패턴(Prototype Pattern)의 기본 개념 정리 (C++ 샘플코드 포함)"
excerpt: Prototype Pattern

categories:
  - Design Pattern
tags:
  - [Design Pattern, Prototype, Prototype Pattern, 프로토타입 패턴, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2024-10-15
last_modified_at: 2024-10-15
---

## 프로토타입(Prototype)이란?
---
프로토타입 패턴은 기존 객체(프로토타입)를 복사하여 새로운 객체를 생성하는 디자인 패턴입니다. <br>
```new``` 키워드를 사용하여 객체를 직접 생성하는 대신, 기존 객체를 복제함으로써 객체 생성 과정을 간소화하고 성능을 향상시킬 수 있습니다. <br>
특히, 객체 생성 과정이 복잡하거나 비용이 많이 드는 경우, 또는 생성할 객체의 구체적인 클래스를 런타임에 결정해야 하는 경우에 유용합니다.

<br><br>

### 구성요소
---
* Prototype (프로토타입): 복제할 객체의 인터페이스 또는 추상 클래스를 정의합니다. ```clone()```과 같은 복제 메서드를 선언합니다.
* ConcretePrototype (구체적인 프로토타입): 프로토타입 인터페이스를 구현하는 구체적인 클래스입니다. 자신을 복제하는 clone() 메서드를 구현합니다.
* Client (클라이언트): 프로토타입을 사용하여 새로운 객체를 생성하는 클래스입니다.

<br><br>

### 프로토타입(Prototype) 패턴의 동작 방식
---
1. 클라이언트는 프로토타입 객체를 가지고 있습니다.
2. 클라이언트가 새로운 객체를 생성해야 할 때, 프로토타입 객체의 ```clone()``` 메서드를 호출합니다.
3. ```clone()``` 메서드는 자신(프로토타입)의 복사본을 생성하여 반환합니다. 이 때, 얕은 복사(shallow copy) 또는 깊은 복사(deep copy)를 사용할 수 있습니다.
4. 클라이언트는 복제된 객체를 사용하여 필요한 작업을 수행합니다.

<br>

### 프로토타입(Prototype) 패턴의 장단점
---
#### 장점
* 객체 생성 과정 단순화: 복잡한 객체 생성 과정을 숨기고, 간단하게 복제를 통해 객체를 생성할 수 있습니다.
* 성능 향상: ```new``` 연산자를 반복적으로 사용하는 것보다 기존 객체를 복제하는 것이 더 효율적일 수 있습니다. 특히, 객체 생성 비용이 높은 경우 성능 향상 효과가 큽니다.
* 런타임 객체 타입 결정: 런타임에 생성할 객체의 종류를 결정할 수 있습니다.
* 클래스 수정 없이 객체 추가 가능: 새로운 객체 타입을 추가하더라도 기존 코드를 수정할 필요가 없습니다. 새로운 프로토타입 클래스를 추가하고 클라이언트에서 해당 프로토타입을 사용하도록 변경하면 됩니다.

#### 단점
* 복잡한 객체의 경우 복제 구현이 어려울 수 있음: 객체의 구조가 복잡한 경우, 깊은 복사를 구현하는 것이 어려울 수 있습니다. 특히, 순환 참조가 있는 경우 복제 로직이 더욱 복잡해집니다.
* 클래스 계층 구조가 복잡해질 수 있음: 프로토타입이 많아지면 클래스 계층 구조가 복잡해질 수 있습니다.
<br><br>

### 구현
---

```C++
#include <iostream>
#include <string>

class Shape { // 프로토타입 인터페이스
public:
    virtual ~Shape() {}
    virtual Shape* clone() = 0;
    virtual void draw() = 0;
};

class Rectangle : public Shape { // 구체적인 프로토타입
private:
    int width_;
    int height_;

public:
    Rectangle(int width, int height) : width_(width), height_(height) {}
    Rectangle(const Rectangle& other) : width_(other.width_), height_(other.height_) { // 복사 생성자 (깊은 복사)
        std::cout << "Rectangle copy constructor called" << std::endl;
    }
    ~Rectangle(){
        std::cout << "Rectangle destructor called" << std::endl;
    }

    Shape* clone() override {
        return new Rectangle(*this); // 복사 생성자를 이용한 복제 (깊은 복사)
    }

    void draw() override {
        std::cout << "Drawing a rectangle with width " << width_ << " and height " << height_ << std::endl;
    }
};

class Circle : public Shape { // 또 다른 구체적인 프로토타입
private:
    int radius_;

public:
    Circle(int radius) : radius_(radius) {}
    Circle(const Circle& other) : radius_(other.radius_) { // 복사 생성자 (깊은 복사)
        std::cout << "Circle copy constructor called" << std::endl;
    }
    ~Circle(){
        std::cout << "Circle destructor called" << std::endl;
    }
    Shape* clone() override {
        return new Circle(*this); // 복사 생성자를 이용한 복제 (깊은 복사)
    }

    void draw() override {
        std::cout << "Drawing a circle with radius " << radius_ << std::endl;
    }
};

int main() {
    Rectangle* rect = new Rectangle(10, 20);
    Shape* rectClone = rect->clone();
    rectClone->draw(); // Drawing a rectangle with width 10 and height 20
    delete rect;
    delete rectClone;
    std::cout << std::endl;

    Circle* circle = new Circle(5);
    Shape* circleClone = circle->clone();
    circleClone->draw(); // Drawing a circle with radius 5
    delete circle;
    delete circleClone;

    return 0;
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}