---
title: "[Design Pattern] 데코레이터 패턴(Decorator Pattern)의 기본 개념 정리 (C++ 샘플코드 포함)"
excerpt: Decorator Pattern이란

categories:
  - Design Pattern
tags:
  - [Design Pattern, Decorator, Decorator Pattern, 데코레이터 패턴]

toc: true
toc_sticky: true
 
date: 2022-02-13
last_modified_at: 2022-02-13
---

## 데코레이터 패턴이란?
---
데코레이터 패턴은 객체의 기능을 동적으로 확장하기 위한 구조 디자인 패턴입니다. 기존 객체의 코드를 수정하지 않고, 래퍼(wrapper) 객체를 사용하여 기능을 추가합니다. <br>
여러 개의 데코레이터를 체인처럼 연결하여 다양한 조합의 기능을 추가할 수 있습니다.
<br><br>

![UML_class_diagram](https://user-images.githubusercontent.com/40765022/153752435-cadf59ac-f5d0-4a7e-848b-f9edf16daa7c.png)

##### (이미지 출처 : https://en.wikipedia.org/wiki/Decorator_pattern) <br> <br>

### 구성요소
---
* Component (컴포넌트): 기능을 추가할 객체의 인터페이스를 정의합니다.
* ConcreteComponent (구체적인 컴포넌트): 실제 기능을 제공하는 객체입니다. 데코레이터가 기능을 추가할 대상입니다.
* Decorator (데코레이터): Component 인터페이스를 구현하며, Component 객체를 멤버 변수로 가지고 있습니다. 다른 데코레이터들의 기본 클래스 역할을 합니다.
* ConcreteDecorator (구체적인 데코레이터): Decorator를 상속받아 실제 기능을 추가합니다.
 
### Decorator Pattern의 동작 방식
---
1. 클라이언트가 ConcreteComponent 객체를 생성합니다.
2. 클라이언트는 필요한 기능을 추가하기 위해 ConcreteDecorator 객체를 생성하고, 생성 시점에 ConcreteComponent 객체를 전달합니다.
3. ConcreteDecorator는 Component 인터페이스의 메서드를 구현하면서, 자신의 기능을 수행하기 전이나 후에 Component 객체의 메서드를 호출합니다. 이를 통해 기능을 추가합니다.
4. 여러 개의 ConcreteDecorator를 사용하여 기능을 체인처럼 연결할 수 있습니다.
<br><br>

### Decorator Pattern의 장단점
---
#### 장점
* 개방-폐쇄 원칙(Open/Closed Principle) 준수: 기존 코드를 수정하지 않고 새로운 기능을 추가할 수 있습니다.
* 유연성: 런타임에 동적으로 기능을 추가하거나 제거할 수 있습니다.
* 코드 중복 방지: 기능을 모듈화하여 코드 중복을 줄일 수 있습니다.
* 상속의 대안: 상속을 과도하게 사용할 경우 발생할 수 있는 클래스 폭발 문제를 해결할 수 있습니다.

#### 단점
* 많은 작은 클래스가 생성될 수 있습니다. 특히 추가할 기능이 많을 경우 클래스 수가 증가할 수 있습니다.
* 객체 구성이 복잡해질 수 있습니다. 많은 데코레이터가 체인처럼 연결될 경우 객체 구성을 이해하기 어려울 수 있습니다.


<br><br>

## 예제
---

``` C++
#include <iostream>
#include <string>

// Component 인터페이스
class Coffee {
public:
    virtual ~Coffee() {}
    virtual std::string getDescription() const = 0;
    virtual double getCost() const = 0;
};

// ConcreteComponent: 기본 커피
class SimpleCoffee : public Coffee {
public:
    std::string getDescription() const override {
        return "Simple Coffee";
    }
    double getCost() const override {
        return 1.0;
    }
};

// Decorator 추상 클래스
class CoffeeDecorator : public Coffee {
protected:
    Coffee* coffee;
public:
    CoffeeDecorator(Coffee* coffee) : coffee(coffee) {}
    std::string getDescription() const override {
        return coffee->getDescription();
    }
    double getCost() const override {
        return coffee->getCost();
    }
};

// ConcreteDecorator: 우유 추가
class MilkDecorator : public CoffeeDecorator {
public:
    MilkDecorator(Coffee* coffee) : CoffeeDecorator(coffee) {}
    std::string getDescription() const override {
        return CoffeeDecorator::getDescription() + ", Milk";
    }
    double getCost() const override {
        return CoffeeDecorator::getCost() + 0.5;
    }
};

// ConcreteDecorator: 설탕 추가
class SugarDecorator : public CoffeeDecorator {
public:
    SugarDecorator(Coffee* coffee) : CoffeeDecorator(coffee) {}
    std::string getDescription() const override {
        return CoffeeDecorator::getDescription() + ", Sugar";
    }
    double getCost() const override {
        return CoffeeDecorator::getCost() + 0.2;
    }
};

int main() {
    Coffee* coffee = new SimpleCoffee();
    std::cout << coffee->getDescription() << " Cost: $" << coffee->getCost() << std::endl;

    Coffee* milkCoffee = new MilkDecorator(coffee);
    std::cout << milkCoffee->getDescription() << " Cost: $" << milkCoffee->getCost() << std::endl;

    Coffee* milkSugarCoffee = new SugarDecorator(milkCoffee);
    std::cout << milkSugarCoffee->getDescription() << " Cost: $" << milkSugarCoffee->getCost() << std::endl;

    delete coffee;
    delete milkCoffee;
    delete milkSugarCoffee;

    return 0;
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}