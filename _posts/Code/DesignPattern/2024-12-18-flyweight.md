---
title:  "[Design Pattern] 플라이웨이트(Flyweight) 패턴"
excerpt: Finite State Machine Pattern

categories:
  - Design Pattern
tags:
  - [Design Pattern, Flyweight, Flyweight Pattern, 플라이웨이트 패턴, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2025-01-15
last_modified_at: 2025-01-15
---

## 플라이웨이트(Flyweight) 패턴이란?
---
플라이웨이트 패턴은 많은 수의 유사한 객체를 생성해야 할 때, 객체의 일부 상태를 공유하여 메모리 사용량을 최소화하는 구조 디자인 패턴입니다. "플라이웨이트(flyweight)"는 "가벼운 무게"를 의미하며, 이름처럼 객체를 가볍게 만들어 메모리 낭비를 줄이는 것이 목적입니다. 마치 군대에서 군인들이 공통된 군복을 입는 것과 같습니다. <br>각 군인마다 모든 군복을 개별적으로 가지고 있는 것이 아니라, 공통된 군복 디자인을 공유하여 옷을 생산하고 관리하는 비용을 줄이는 것처럼, 플라이웨이트 패턴은 객체의 공통 부분을 공유하여 메모리 사용량을 줄입니다.

<br><br>

### 플라이웨이트(Flyweight) 패턴의 구성 요소
---
* Flyweight (플라이웨이트): 공유될 수 있는 객체의 부분을 나타내는 인터페이스 또는 추상 클래스입니다. 내부 상태(Intrinsic State)를 저장합니다.
* Concrete Flyweight(구체적인 플라이웨이트): ```Flyweight 인터페이스```를 구현하는 클래스입니다. 공유되는 객체의 실제 구현을 담당합니다. 모든 ```Concrete Flyweight```객체는 동일한 내부 상태를 공유합니다.
* Unshared Concrete Flyweight(공유되지 않는 구체적인 플라이웨이트 - 선택적): 공유될 수 없는 상태를 가진 객체를 나타냅니다. 플라이웨이트 패턴을 적용할 수 없는 경우에 사용됩니다.
* Flyweight Factory(플라이웨이트 팩토리): 플라이웨이트 객체를 생성하고 관리하는 역할을 합니다. 이미 생성된 플라이웨이트 객체가 있다면 재사용하고, 없다면 새로 생성합니다.
* Client(클라이언트): 플라이웨이트 객체를 사용하는 객체입니다. 외부 상태(Extrinsic State)를 플라이웨이트 객체에 전달하여 객체의 동작을 결정합니다.
<br><br>

### 플라이웨이트(Flyweight) 패턴의 작동 방식
---
1. 클라이언트는 플라이웨이트 팩토리에 필요한 내부 상태를 요청합니다.
2. 플라이웨이트 팩토리는 해당 내부 상태를 가진 플라이웨이트 객체가 이미 생성되어 있는지 확인합니다.
3. 이미 생성된 객체가 있다면 해당 객체를 반환하고, 없다면 새로운 객체를 생성하여 반환합니다.
4. 클라이언트는 반환받은 플라이웨이트 객체와 함께 외부 상태를 사용하여 작업을 수행합니다.
<br><br>

### 내부 상태 (Intrinsic State) 와 외부 상태 (Extrinsic State)
---
* 내부 상태: 객체 내부에서 저장되고 공유되는 상태입니다. 이 상태는 플라이웨이트 객체 간에 공유됩니다. 예를 들어, 폰트의 글꼴, 크기, 스타일 등이 내부 상태에 해당할 수 있습니다.
* 외부 상태: 객체마다 다르고 공유되지 않는 상태입니다. 이 상태는 클라이언트에서 플라이웨이트 객체에 전달됩니다. 예를 들어, 텍스트의 위치, 색상, 내용 등이 외부 상태에 해당할 수 있습니다.
<br><br>

### 플라이웨이트(Flyweight) 패턴의 장단점
---
#### 장점
* 메모리 사용량 감소: 객체의 공통 부분을 공유함으로써 메모리 사용량을 크게 줄일 수 있습니다.
* 성능 향상: 객체 생성 및 관리 비용을 줄여 성능을 향상시킬 수 있습니다.

#### 단점
* 코드 복잡성 증가: 패턴 적용으로 인해 코드의 구조가 다소 복잡해질 수 있습니다.
* 공유 상태 관리의 어려움: 공유되는 내부 상태를 변경하는 경우, 모든 클라이언트에 영향을 미치므로 주의해야 합니다.
<br><br>


### 활용 예시
---
* 텍스트 편집기: 각 문자를 플라이웨이트로 표현하여 메모리 사용량을 줄입니다.
* 게임: 많은 수의 동일한 오브젝트 (예: 나무, 풀, 건물)를 표현할 때 사용합니다.
* 캐릭터 에디터: 의상, 액세서리 등을 플라이웨이트로 표현하여 메모리 사용량을 최적화합니다.
<br><br>

## 예시코드
---

```C++
#include <iostream>
#include <map>

// 플라이웨이트 인터페이스
class Character {
public:
    virtual void Draw(int x, int y) = 0;
    virtual ~Character() {}
};

// 구체적인 플라이웨이트
class ConcreteCharacter : public Character {
private:
    char value_;
public:
    ConcreteCharacter(char value) : value_(value) {}
    void Draw(int x, int y) override {
        std::cout << "Character: " << value_ << " at (" << x << ", " << y << ")" << std::endl;
    }
};

// 플라이웨이트 팩토리
class CharacterFactory {
private:
    std::map<char, Character*> characters_;
public:
    Character* GetCharacter(char value) {
        if (characters_.find(value) == characters_.end()) {
            characters_[value] = new ConcreteCharacter(value);
        }
        return characters_[value];
    }
    ~CharacterFactory(){
        for(auto const& [key, val] : characters_){
            delete val;
        }
    }
};

int main() {
    CharacterFactory factory;

    // 외부 상태 (위치)
    int x = 10;
    int y = 20;

    // 같은 문자 'A'를 여러 번 사용
    Character* charA1 = factory.GetCharacter('A');
    charA1->Draw(x, y);
    x += 10;

    Character* charA2 = factory.GetCharacter('A'); // 기존 객체 재사용
    charA2->Draw(x, y);
    x += 10;

    Character* charB = factory.GetCharacter('B');
    charB->Draw(x, y);

    return 0;
}
```

[Top](#){: .btn .btn--primary }{: .align-right}