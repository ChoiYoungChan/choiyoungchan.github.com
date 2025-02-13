---
title:  "[Unity] 유니티에서 사용하는 여러가지 Singleton Pattern 방법"
excerpt: Unity에서 사용하는 Singleton Pattern

categories:
  - Unity Code
tags:
  - [Design Pattern, Singleton, Unity, 싱글톤]

toc: true
toc_sticky: true
 
date: 2022-01-15
last_modified_at: 2022-01-15
---

https://choiyoungchan.github.io/design%20pattern/singleton/

싱글톤 패턴의 사용 이유와 개념은 위의 포스팅을 참조

## 사용법
---
싱글톤 패턴을 구현하는 방법은 여러가지가 있으나 기본적으로 Static형 인스턴스를 1개 생성한다는점에서 공통점이 있으며, Unity에서 활용 가능한 싱글톤 패턴을 4가지 정도 소개하고자 합니다. <br>
경우와 상황에 따라 변형 하여 사용하는 경우도 많이 있습니다. <br>

- 일반적인 싱글톤
- MonoBehaviour를 사용한 싱글톤
- Generic을 활용, MonoBehaviour를 사용 하는 싱글톤
- Generic을 활용, MonoBehaviour를 사용 하지않는 싱글톤
<br><br>

### 예시 코드
--- 

[일반적인 싱글톤]
```c#
using UnityEngine;
using System;

public class Singleton
{
    private static Singleton instance;

    public static Singleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new Singleton();
            }
            return instance;
        }
    }

    /// <summary>
    /// Constructor
    /// </summary>
    public Singleton()
    {
        // You can do any settings what you need
    }

    public void FuncWhatYouNeed()
    {
        // You can write down any Function what you need Like Pause Game or Restart. Initialize
    }
}
```
<br><br>

[MonoBehaviour를 사용한 싱글톤]
```c#
public abstract class Singleton : MonoBehaviour
{
    private static Singleton instance;

    public static Singleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new Singleton();
            }
            return instance;
        }
    }

    /// <summary>
    /// Constructor
    /// </summary>
    public Singleton()
    {
        // You can do any settings what you need
    }

    public void FuncWhatYouNeed()
    {
        // You can write down any Function what you need Like Pause Game or Restart. Initialize
    }
}
```
<br><br>

[Generic을 활용, MonoBehaviour를 사용 하는 싱글톤]
```c#
public abstract class Singleton<T> : MonoBehaviour where T : MonoBehaviour
{
    private static T m_instance;

    public static T Instance
    {
        get
        {
            if (m_instance == null)
            {
                Type t = typeof(T);
                m_instance = (T)FindObjectOfType(t);

                if (m_instance == null)
                {
                    m_instance = new GameObject(typeof(T).ToString(), typeof(T)).AddComponent<T>();
                }

                return m_instance;
            }
        }
    }
}
```
<br><br>

[Generic을 활용, MonoBehaviour를 사용 하지않는 싱글톤]
```c#
/// <summary>
/// Monobehavior를 사용 하지 않는 Singleton
/// </summary>
/// <typeparam name="T"></typeparam>

public class Singleton<T> where T : class
{
    private static T m_instance;

    public static T Instance
    {
        get
        {
            if (m_instance == null)
            {
                m_instance = Activator.CreateInstance(typeof(T)) as T;
            }
            return m_instance;
        }
    }
}
```
<br><br>

## 문제점&주의사항
---
- 싱글톤의 역할이 커질 수록 결합도가 높아져서 객체 지향 설계 원칙(개방-폐쇄 원칙)에 어긋날 수 있다.
- 객체의 파괴 시점을 컨트롤 하기 어려워질 수 있다.
- 멀티쓰레드 환경에서 컨트롤이 어렵다.
<br>

[Top](#){: .btn .btn--primary }{: .align-right}