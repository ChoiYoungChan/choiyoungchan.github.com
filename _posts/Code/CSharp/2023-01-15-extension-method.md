---
title:  "[C#] C#에서 확장 Method(Extension Method)사용법과 설명 완벽 정리 (C# 예시 코드 포함)"
excerpt: Extension Method in C#

categories:
  - C Sharp
tags:
  - [C#, Extension Method, 확장 Method]

toc: true
toc_sticky: true
 
date: 2023-01-15
last_modified_at: 2023-01-15
---

## 확장 Method(Extension Method) 개념
--- 
기존 클래스를 수정하지 않고 새로운 매소드를 추가하는 기능입니다. <br>
일반적으로 확장 메소드는 기존 클래스를 확장하는 Static 메소드 이며, 기존 객체를 사용하여 호출할 수 있지만 Static클래스에 정의됩니다.<br> 

간단하게 설명하자면….스마트폰에 폰케이스나 필름 등 악세사리를 추가하는것과 비슷합니다. 스마트폰을 분해하지 않고도 좋은 기능을 추가할 수 있습니다. <br>

주로 기존 코드를 수정하지 않고 기능을 확장할때, 예를들어 이미 정의된 클래스 또는 라이브러리에 새로운 기능을 추가할 때 사용됩니다.(당연하게도…)

<br><br>

### 예제
--- 

[샘플 코드]
```c#
public static class Extension
{
  public static string MakeFirstLetterUpperCase(string input)
  {
    if(string.IsNullOrEmpty(input)) return input;

    return char.ToUpper(input[0] + input.Substring(1));
  }
}
```
<br>

[전체 코드]
```c#
using System;

public static class StringExtension
{
    public static string MakeFirstLetterUpperCase(this string input)
    {
        if (string.IsNullOrEmpty(input)) return input;

        return char.ToUpper(input[0]) + input.Substring(1);
    }
}

public class Program
{
    public static void Main()
    {
        string input = "hello, world!";
        string output = input.MakeFirstLetterUpperCase();
        Console.WriteLine(output); // Output: "Hello, world!"
    }
}

```
<br>

### 잘못된 사용법
확장 메소드를 잘못 사용하는 경우도 있습니다.<br>
아래와 같이 Static메소드처럼 호출 하는것이 잘못 사용하는것이며, 상기처럼 인스턴스 메소드 처럼 호출되어야 합니다.<br>

```c#
public static void Main()
{
  string input = "hello, world!";
  string output = StringExtension.MakeFirstLetterUpperCase(example, "Hello, "); // 정적 메서드로 호출했음.
  Console.WriteLine(output); // Output: "Hello, world!"
}
```
<br>


## 주의 사항
* Extension Method는 정적 클래스에 정의되어야 합니다.
* 메서드의 첫 번째 매개 변수는 this 키워드와 함께 사용되어야 합니다.
* 확장 메서드를 사용하는 것은 해당 클래스를 직접 수정하는 것보다 선호되지 않을 수 있습니다. 
  이는 클래스가 개방형으로 설계되어 있지 않고, 확장 메서드를 사용하면 코드의 가독성이 떨어질 수 있기 때문입니다.


<br>

[Top](#){: .btn .btn--primary }{: .align-right}