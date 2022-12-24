---
title:  "[C#] Partial Class"
excerpt: C# 에서 사용하는 Partial Class

categories:
  - C Sharp
tags:
  - [C#, Partial Class, 클래스를 나눠서, 부분 클래스]

toc: true
toc_sticky: true
 
date: 2022-11-27
last_modified_at: 2022-11-27
---

## 개요
Partial Class란?<br>
=> Partial Class는 C# 2.0에 도입된 기능으로 클래스를 여러 파일에 분할하여 정의할 수 있는 클래스 입니다. <br>
클래스의 내용을 다른 파일로 분할할 수 있지만, 응용 프로그램이 컴파일될 때 분할된 파일이 결합되기 때문에 논리적으로는 하나입니다. <br>

규모가 큰 개발 환경에서는 간혹 볼 수도 있지만 실제로는 많이 사용되지 않으니
간략히 이런 개념이다 정도로 이해하시는 정도로 충분하다고 생각합니다. <br>


장점<br>
- 큰 클래스를 분할하여 여러 개발자가 사용할 수 있다
- 규모가 큰 개발에서 접근 권한, Complict등의 문제 발생을 줄일 수 있다.
 
단점<br>
- 가독성을 해친다
- 디버깅시 Break Point로 쫒아가기 힘들다
- 이름이 다른 같은 기능의 메소드가 중복 가능성이 있다.<br>
  (A클래스의 이미지 로딩 함수 1, B클래스 이미지 로딩 함수 2)

사용시 주의점<br>
- 다중상속을 지원하지 않습니다.
- 분할된 파일은 모두 partial키워드를 사용해야 합니다.
- 메소드는 반드시 void를 return 해야한다.
  
--- 
 <br>

### 예제
--- 

아래의 예시에서는 car01, car02라는 cs파일에 클래스를 분할한 예시 입니다.  <br> 
 <br> 

[Car01.cs]
```c#
partial class Car
{
  private string _name;
  private int _year;

  public void DisplayCarInfo()
  {
    Consol.WriteLine("Name : " + _name + " " + "Year : " + _year);
  }
}
```

 <br> 

[Car02.cs]
```c#
partial class Car
{
  public string Name
  {
    get { return _name; }
    set{ _name = value; }
  }

  public string Year
  {
    get { return _year; }
    set{ _year = value; }
  }
}
```

<br> 

[Main.cs]
```c#
class Example
{
  void Main()
  {
    Car _car = new Car();
    _car.name = "Volvo_XC90";
    _car.year = 2022;

    _car.DisplayCarInfo();
  }
}
```


#### build result

```
 Name : Volvo_XC90 Year : 2021
```

<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}