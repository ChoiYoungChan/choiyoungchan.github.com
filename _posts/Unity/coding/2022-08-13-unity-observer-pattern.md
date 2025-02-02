---
title:  "[Unity] 유니티에서 사용하는 관찰자 패턴(Observer Pattern)"
excerpt: Observer Pattern in Unity

categories:
  - Unity Code
tags:
  - [Design Pattern, Observer, Unity, 관찰자]

toc: true
toc_sticky: true
 
date: 2022-08-27
last_modified_at: 2022-08-27
---

## 관찰자 패턴(Observer Pattern)이란?
---
옵저버 패턴은 한 객체(주체, Subject)의 상태가 변경될 때, 그 객체에 의존하는 다른 객체들(관찰자, Observer)에게 자동으로 통지하도록 하는 디자인 패턴입니다. <br>
주체는 관찰자 목록을 유지하고, 상태가 변경될 때마다 이 목록을 순회하며 각 관찰자에게 업데이트를 알립니다.<br>

자세한 사용 이유와 개념은 이쪽 포스팅을 참조 -> [Observer Pattern](https://choiyoungchan.github.io/design%20pattern/observer/)

<br><br>

### 유니티 이벤트 시스템과의 비교
---
유니티는 자체적인 이벤트 시스템을 제공합니다. <br>
관찰자 패턴은 더욱 유연하고 확장성이 뛰어나지만, 간단한 이벤트 처리에는 유니티 이벤트 시스템을 사용하는 것이 더 간편할 수 있습니다.

<br>

### 장점
---
* 느슨한 결합: 객체 간의 의존성을 줄여 코드 유지보수가 용이합니다.
* 확장성: 새로운 관찰자를 쉽게 추가하거나 제거할 수 있습니다.
* 재사용성: 다양한 상황에 적용할 수 있는 유연한 패턴입니다.

<br>

### 활용 예시
---
* UI 업데이트: 게임 오브젝트의 상태가 변경될 때 UI를 업데이트합니다.
* 이벤트 시스템: 특정 이벤트 발생 시 여러 스크립트에 알림을 전달합니다.
* 게임 로직: 게임 오브젝트 간의 상호 작용을 관리합니다.

<br>

### 주의 사항
---
* 메모리 누수: 관찰자를 등록하고 해제하는 것을 잊으면 메모리 누수가 발생할 수 있습니다.
* 성능: 많은 관찰자가 등록된 경우 성능 저하가 발생할 수 있습니다.
* 순환 참조: 주체와 관찰자가 서로를 참조하는 경우 무한 루프에 빠질 수 있습니다.

<br>

## 사용법
---

1. 델리게이트와 이벤트 선언
   * 델리게이트: 관찰자가 구현해야 할 메서드의 시그니처를 정의합니다.
   * 이벤트: 델리게이트를 통해 관찰자들에게 알림을 보내는 메커니즘입니다.
```C#
public class Subject : MonoBehaviour
{
    public delegate void OnStateChanged();
    public event OnStateChanged OnStateChangedEvent;

    // 상태 변경 메서드
    public void ChangeState()
    {
        // 상태 변경 로직
        OnStateChangedEvent?.Invoke();
    }
}
```
<br>

2. 관찰자 등록 및 해제:
   * 등록: Subject의 이벤트에 관찰자의 메서드를 추가합니다.
   * 해제: Subject의 이벤트에서 관찰자의 메서드를 제거합니다.

```C#
public class Observer : MonoBehaviour
{
    private Subject subject;

    void Start()
    {
        subject = FindObjectOfType<Subject>();
        subject.OnStateChangedEvent += HandleStateChanged;
    }

    void OnDestroy()
    {
        subject.OnStateChangedEvent -= HandleStateChanged;
    }

    void HandleStateChanged()
    {
        // 상태 변경에 따른 처리 로직
    }
}
```
<br>

3. 상태 변경 시 알림:
   * Subject의 상태가 변경될 때 OnStateChangedEvent를 호출하여 모든 관찰자에게 알립니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}