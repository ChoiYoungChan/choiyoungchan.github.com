---
title:  "[C#] Interface란"
excerpt: C# 에서 사용하는 Interface란

categories:
  - C Sharp
tags:
  - [C#, Interface, 인터페이스]

toc: true
toc_sticky: true
 
date: 2022-12-10
last_modified_at: 2022-12-10
---

## 개요
Interface란?<br>
=> 한마디로 인터페이스는 Method 원형들의 집합에 이름을 붙인 것으로,  상속 받을 클래스에 기능이나 속성을 지정하는 역할을 합니다. <br>
인터페이스는 추상클래스와 매우 유사하며, 인터페이스에서는 Method를 선언하고  실체는 클래스가 상속 받아 인터페이스의 Method를 구현하는 방식입니다.

추상 클래스와 차이점은 추상클래스는 다중상속을 지원하지 않지만 인터페이스는 다중상속을 지원하며, 인터페이스 자체로 인스턴스 생성이 안된다는 특징이 있습니다.<br>
<br>

인터페이스를 사용해야 하는 이유는 다음과 같습니다.<br>
1. 외부 시스템에 제공할 서비스 또는 객체 정보를 직접적인 class가 아닌 "선언" 만을 제공한다.
2. 다중 상속에 따른 class의 표현을 여러가지로 가능하게 한다.
3. 의도하지 않은 속성/Method 공개를 막기 위해서도 사용한다.
4. 실제 object 의 class 정보를 제공하고 싶지 않을 때 혹은 명확히 하고 싶을 때 사용한다. 
<br><br>

### 예제
--- 

다음과 같이 interface라고 선언후 Interface의 약자인 I + 인터페이스 이름 형식으로 지정후 필요 Method를 선언하시면됩니다.
``` C#
interface IMessage
{
    void DisplayMessage();
    void SetMessage(string _text);
}
```
 <br> 
인터페이스를 상속 받은 클래스에서 인터페이스의 Method를 구현

``` C#
class MessageBox : IMessage
{
    private string _message;
    public void DisplayMessage()
    {
        Console.WriteLine(_message);
    }

    public void SetMessage(string _text)
    {
        _message = _text;
    }
}

class TextMessage : IMessage
{
    private string _message;
    public void DisplayMessage()
    {
        Console.WriteLine(_message);
    }

    public void SetMessage(string _text)
    {
        _message = _text;
    }
}
```

<br> 
전체 소스코드

InterFace
``` C#
interface IMessage
{
    void DisplayMessage();
    void SetMessage(string _text);
}
```

Main Class
``` C#
using System;

class MessageBox : IMessage
{
    private string _message;
    public void DisplayMessage()
    {
        Console.WriteLine(_message);
    }

    public void SetMessage(string _text)
    {
        _message = _text;
    }
}

class TextMessage : IMessage
{
    private string _message;
    public void DisplayMessage()
    {
        Console.WriteLine(_message);
    }

    public void SetMessage(string _text)
    {
        _message = _text;
    }
}

class MainClass
{
    public static void Main(string[] args)
    {
        MessageBox _messageBox = new MessageBox();
        TextMessage _textMessage = new TextMessage();

        _messageBox.SetMessage("I Love Dog");
        _textMessage.SetMessage("More then Cat");

        _messageBox.DisplayMessage();
        _textMessage.DisplayMessage();
    }
}
```


### build result

```
I Love Dog
More then Cat
```

<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}