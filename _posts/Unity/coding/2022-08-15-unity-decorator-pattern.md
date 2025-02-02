---
title:  "[Unity] 유니티에서 사용하는 장식자 패턴(Decorator Pattern)"
excerpt: Decorator Pattern in Unity

categories:
  - Unity Code
tags:
  - [Design Pattern, Decorator, 장식자 패턴, 데코레이터]

toc: true
toc_sticky: true
 
date: 2022-01-15
last_modified_at: 2022-01-15
---

## 장식자 패턴(Decorator Pattern)이란?
---
장식자 패턴은 객체에 기능을 동적으로 추가하는 디자인 패턴입니다. 기존 객체의 기능을 변경하거나 새로운 기능을 추가할 때 서브클래스를 만들어 상속하는 대신, 기존 객체를 감싸서 기능을 확장하는 방식입니다. <br>
이를 통해 유연하고 확장 가능한 코드를 구현할 수 있습니다.<br>

자세한 사용 이유와 개념은 이쪽 포스팅을 참조 -> [Decorator Pattern](https://choiyoungchan.github.io/design%20pattern/decorator/)

<br><br>

### 유니티 이벤트 시스템과의 비교
---
유니티는 자체적인 이벤트 시스템을 제공합니다. <br>
관찰자 패턴은 더욱 유연하고 확장성이 뛰어나지만, 간단한 이벤트 처리에는 유니티 이벤트 시스템을 사용하는 것이 더 간편할 수 있습니다.

<br>

### 장점
---
* 유연성: 런타임에 동적으로 기능을 추가하거나 제거할 수 있습니다.
* 확장성: 새로운 기능을 추가하기 위해 기존 코드를 수정할 필요가 없습니다.
* 재사용성: 다양한 객체에 동일한 장식자를 적용할 수 있습니다.

<br>

### 단점
---
* 복잡성: 코드가 다소 복잡해질 수 있습니다.
* 성능 오버헤드: 여러 개의 장식자가 겹쳐질 경우 성능이 저하될 수 있습니다.

<br>

### 활용 예시
---
* 게임 오브젝트에 다양한 효과 추가: 무기에 데미지 증가, 범위 공격 등의 효과를 추가할 수 있습니다.
* 네트워크 통신: 패킷 암호화, 압축 등의 기능을 추가할 수 있습니다.
* 로그 기록: 메서드 실행 시간 측정, 로그 기록 등을 추가할 수 있습니다.

<br>


## 사용법
---

1. 컴포넌트 인터페이스 정의:

```C#
public interface IComponent
{
    void DoSomething();
}
```
<br>

2. 기본 컴포넌트 구현:

```C#
public class BaseComponent : MonoBehaviour, IComponent
{
    public virtual void DoSomething()
    {
        Debug.Log("BaseComponent: DoSomething");
    }
}
```
<br>

3. 장식자 클래스 구현:
```C#
public class Decorator : MonoBehaviour, IComponent
{
    private IComponent component;

    public Decorator(IComponent component)
    {
        this.component = component;
    }

    public virtual void DoSomething()
    {
        component.DoSomething();
        // 추가 기능
        Debug.Log("Decorator: Additional functionality");
    }
}
```

4. 다양한 장식자 클래스 생성:
```C#
public class LoggingDecorator : Decorator
{
    public LoggingDecorator(IComponent component) : base(component) {}

    public override void DoSomething()
    {
        Debug.Log("Logging before");
        base.DoSomething();
        Debug.Log("Logging after");
    }
}

public class TimingDecorator : Decorator
{
    public TimingDecorator(IComponent component) : base(component) {}

    public override void DoSomething()
    {
        Stopwatch stopwatch = new Stopwatch();
        stopwatch.Start();
        base.DoSomething();
        stopwatch.Stop();
        Debug.Log($"Elapsed time: {stopwatch.ElapsedMilliseconds}ms");
    }
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}