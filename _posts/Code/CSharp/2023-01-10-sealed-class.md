---
title:  "[C#] C#에서 봉인 클래스 및 봉인 Method"
excerpt: Sealed Class and Sealed Method in C#

categories:
  - C Sharp
tags:
  - [C#, Sealed Class, Sealed Method, 봉인 클래스, 봉인 Method]

toc: true
toc_sticky: true
 
date: 2023-01-10
last_modified_at: 2023-01-10
---

## 개념
--- 
### 봉인 클래스(Sealed Class) <br>
만약 클래스가 다른 클래스에 상속되는것을 원하지 않을 떄 해당 클래스를 봉인 클래스로 선언할 수 있으며, 이때 아래와 같이 Sealed키워드로 선언을 합니다.<br>
```c#
sealed class TestClass
```

봉인 클래스의 특징
* 봉인 클래스는 상속을 피하거나 제한하기 위해 고안되었습니다.
* 다른 클래스에 상속될 수 없으므로 상속 계층에서 최하위 클래스여야 합니다.
* 봉인 클래스와 추상 클래스는 다릅니다.
* 봉인 클래스는 추상 Method를 가질 수 없습니다.
* sealed 키워드는 클래스뿐만 아니라 Method, Property에 사용할 수 있습니다.

<br>

추상 클래스와 차이점
* 추상 클래스에는 추상 및 비추상 Method가 존재하지만, 봉인 클래스에는 추상 및 가상 Method가 존재할 수 없습니다.
* 추상 클래스는 직접 인스턴스화할 수 없습니다. 하지만, 봉인 클래스는 인스턴스를 생성할 수 있습니다.
* 추상 클래스를 사용하기 위해서는 확장된 클래스를 만들어야 합니다. 하지만, 봉인된 클래스에서 확장된 클래스를 만드는 것은 불가능합니다.
* 추상 클래스는 상속 계층 구조에서 최하위 클래스가 될 수 없지만, 봉인 클래스는 최하위 클래스여야 합니다.

<br><br>

### 봉인 Method(Sealed Method)
부모 클래스에 정의된 클래스를 자식 클래스에서 재정의할 수 없는것을 봉인 Method(Sealed Method)라고 합니다.  <br>
클래스에서 메서드가 가상(virtual)으로 선언되면 자식 클래스가 Method를 재정의할 수 있습니다. <br>



<br>

## 예제
--- 

간단하게 아래와 같이 sealed class라고 선언 후 작성하는 방식입니다.

```c#
sealed class SealedClass
{
    // Class members here
}
```
<br>


```c#
sealed class Rectangle
{
    private int length;
    private int width;

    public Rectangle(int l, int w)
    {
        length = l;
        width = w;
    }

    public int GetArea()
    {
        return length * width;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Rectangle r = new Rectangle(4, 5);
        Console.WriteLine("Area of rectangle = {0}", r.GetArea());
    }
}
```
<br>




<br>
[Top](#){: .btn .btn--primary }{: .align-right}