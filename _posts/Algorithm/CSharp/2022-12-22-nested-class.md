---
title:  "[C#] C#에서 사용하는 중첩 클래스"
excerpt: InnerClass in C#

categories:
  - C Sharp
tags:
  - [C#, InnerClass, 중첩 클래스]

toc: true
toc_sticky: true
 
date: 2022-12-22
last_modified_at: 2022-12-22
---

## 개요
중첩 클래스란?<br>
=> 클래스 내부에 클래스를 정의 하여 사용하는 구현방식을 말합니다. <br>
중첩 클래스를 이용하여 클래스를 그룹화 할 수 있으며, 클래스의 사용 범위를 제한 할 수 있습니다.<br><br>

중첩 클래스를 사용하는 이유
* 클래스를 논리적으로 그룹화할 수 있습니다.
* 특정 클래스 내부에서만 사용되기 때문에 코드를 더 쉽게 파악할 수 있으며, 유지 관리가 쉽습니다.
* 특정 클래스 내부에서만 사용되므로 클래스 구조가 단순해집니다.

<br>

<br>

### 예제
--- 
아래는 중첩 클래스의 예제 입니다. 클래스명은 간단하게 Outer, Inner Class로 지정하였습니다. <br>

```c#
using System;

public class OuterClass
{
    public void ShowText()
    {
        Console.WriteLine("Test Inner Class by OuterClass");
    }

    public class InnerClass
    {
        public void ShowText()
        {
            Console.WriteLine("Test Inner Class by InnerClass");
        }
    }
}
```
<br>

중첩 클래스는 public으로 선언되어 있기 때문에 아래와 같은 방식으로 외부에서 접근 할 수 있습니다. <br>
당연하지만 중첩 클래스 선언시 public이 아닌 private로 선언될 경우 아래와 같이 외부에서 접근 할 수 없습니다.  <br>

```c#
public class Program
{
    public static void Main()
    {
        OuterClass _outerClass = new OuterClass();
        _outerClass.ShowText();

        // 중첩 클래스 접근 방법
        OuterClass.InnerClass _innerClass = new OuterClass.InnerClass();
        _innerClass.ShowText();
    }
}
```
<br>



<br> 
전체 소스코드

```c#
using System;

public class OuterClass
{
    public void ShowText()
    {
        Console.WriteLine("Test Inner Class by OuterClass");
    }

    public class InnerClass
    {
        public void ShowText()
        {
            Console.WriteLine("Test Inner Class by InnerClass");
        }
    }
}

public class Program
{
    public static void Main()
    {
        OuterClass _outerClass = new OuterClass();
        _outerClass.ShowText();

        OuterClass.InnerClass _innerClass = new OuterClass.InnerClass();
        _innerClass.ShowText();
    }
}
```
<br>

### build result

```
Test Inner Class by OuterClass
Test Inner Class by InnerClass
```

<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}