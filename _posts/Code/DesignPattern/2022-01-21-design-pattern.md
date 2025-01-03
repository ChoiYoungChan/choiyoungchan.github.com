---
title:  "[Design Pattern] Design Pattern"
excerpt: Design Pattern이란

categories:
  - Design Pattern
tags:
  - [Design Pattern, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2022-01-21
last_modified_at: 2022-01-21
---


## 디자인 패턴이란?
---
객체지향 프로그래밍 설계를 할 때 자주 발생하는 문제들을 피하고 효율적인 코드를 만들기 위한 방법. <br>
알고리즘은 아니지만, 소프트웨어 개발 과정중 특정 상황에서 설계의 구조적인 문제를 해결하는 방식이다. <br>
<br>

---
## 디자인 패턴을 사용하는 이유
---
개발의 효율성과 유지보수성, 운용성이 높아지며, 최적화에 도움이 되기때문이다.<br>
<br>

---
## 가장 많이 쓰이는 패턴
---

### 싱글톤(Singleton)
1개의 인스턴스만 생성하고 이후에는 이 인스턴스를 이용해 어디에서든지 참조할 수 있도록 하는 디자인 패턴 <br>
[싱글톤 패턴](https://choiyoungchan.github.io/design%20pattern/singleton/)<br>
<br>


### 프로토타입(Prototype)
인스턴스를 만들어 놓고 복사한 후 필요한 부분만 수정하여 사용하는 패턴.<br>
기존 객체를 복사하여 객체를 생성<br>
[프로토타입 패턴](https://choiyoungchan.github.io/design%20pattern/prototype/) <br>
<br>

### 팩토리(Factory)
상위 클래스에서 객체를 생성할 인터페이스를 정의하고, 하위 클래스에서 생성 하는 패턴 <br>
실제 객체를 생성하는 클래스를 분리할 수 있는 디자인 패턴<br>
[팩토리 패턴](https://choiyoungchan.github.io/design%20pattern/factory/) <br>
<br>

### 추상(Abstract)
구체적인 클래스에 의존하지 않고 서로 연관되거나 의존적인 객체의 조합을 만드는 인터페이스를 제공하는 패턴. <br>
공장을 만드는 상위 공장을 정의, 구체적인 공장을 만들고 이 공장에서 객체를 생성하는 디자인 패턴<br>
[Abstract 패턴]() <br>
<br>

### 데코레이터 (Decorator)
각각의 기능을 담당하느 클래스들과 이 기능을 적용할 클래스를 분리한뒤 필요에 따라 동적으로 각 기능을 적용할 수 있는 디자인 패턴. <br>
필요시 부가기능을 추가 또는 뺄 수 있는 상속의 대안으로 사용된다. <br>
[데코레이터 패턴](https://choiyoungchan.github.io/design%20pattern/decorator/) <br>
<br>

### 반복자(iterator)
반복자를 사용하여 컨테이너의 요소에 접근하는 디지안 패턴.<br>
내부구조를 노출하지 않고 복잡한 객체의 원소를 순차적으로 접근 가능하다.<br>
[반복자 패턴](https://choiyoungchan.github.io/design%20pattern/iterator/) <br>
<br>

### 관찰자(Observer)
한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체들에 연락이 가고 자동으로 내용이 갱신되는 패턴으로<br>
일대 다의 의존성을 가지며 상호작용하는 객체 사이에서는 가능하면 느슨하게 결합하는 디자인 패턴<br>
[관찰자 패턴](https://choiyoungchan.github.io/design%20pattern/observer/) <br>
<br>

### MVC(Model-View-Control)
<br>
[MVC 패턴](https://choiyoungchan.github.io/design%20pattern/mvc/) <br>
<br>

### MVP(Model-View-Presenter)
<br>
[MVP 패턴](https://choiyoungchan.github.io/design%20pattern/mvp/) <br>
<br>

### MVVM(Model-View-ViewModel)
<br>
[MVVM 패턴](https://choiyoungchan.github.io/design%20pattern/mvvm/) <br>
<br>


---
[Top](#){: .btn .btn--primary }{: .align-right
}