---
title:  "[C#] 클래스 형변환(is, as) 설명 및 C# 샘플 코드"
excerpt: Class type conversion

categories:
  - C Sharp
tags:
  - [C#, Cpp, is, as, 형변환, 클래스 형변환]

toc: true
toc_sticky: true
 
date: 2024-12-27
last_modified_at: 2024-12-27
---

## 개요
---
C#에서 클래스 간 형변환을 수행할 때 is와 as 키워드를 사용하여 안전한 변환을 수행할 수 있습니다. is 연산자는 특정 개체가 지정된 형식과 호환되는지 확인하는 데 사용되며, as 연산자는 형 변환을 수행하지만 변환이 실패하면 예외 대신 null을 반환합니다.
<br><br>

### is 연산자
---
* is 연산자는 객체가 특정 클래스 또는 인터페이스의 인스턴스인지 확인하는 데 사용됩니다.
* 변환 가능 여부만 검사하며 실제 변환은 수행하지 않습니다.
* 결과는 true 또는 false로 반환됩니다.
<br><br>

### 샘플 코드
---
```c#
using System;

class Animal { }
class Dog : Animal { }

class Program
{
    static void Main()
    {
        Animal myAnimal = new Dog();
        
        if (myAnimal is Dog)
        {
            Console.WriteLine("myAnimal은 Dog 형식입니다.");
        }
        else
        {
            Console.WriteLine("myAnimal은 Dog 형식이 아닙니다.");
        }
    }
}
```

[출력]
```
myAnimal은 Dog 형식입니다.
```

<br><br>

### as 연산자
---
* as 연산자는 형 변환을 수행하지만 변환이 실패하면 null을 반환합니다.
* is 연산자와 달리 실제 형 변환이 일어납니다.
* InvalidCastException이 발생하지 않기 때문에 안전한 형 변환이 가능합니다. 단, 값 형식(struct)에는 사용할 수 없습니다.
<br><br>

### 샘플 코드
---
```c#
using System;

class Animal { }
class Dog : Animal { }
class Cat : Animal { }

class Program
{
    static void Main()
    {
        Animal myAnimal = new Dog();
        Dog myDog = myAnimal as Dog;
        Cat myCat = myAnimal as Cat;
        
        if (myDog != null)
        {
            Console.WriteLine("myAnimal은 Dog로 변환되었습니다.");
        }
        else
        {
            Console.WriteLine("myAnimal은 Dog가 아닙니다.");
        }

        if (myCat != null)
        {
            Console.WriteLine("myAnimal은 Cat로 변환되었습니다.");
        }
        else
        {
            Console.WriteLine("myAnimal은 Cat가 아닙니다.");
        }
    }
}
```

[출력]
```
myAnimal은 Dog로 변환되었습니다.
myAnimal은 Cat가 아닙니다.
```
<br>

## is와 as 비교
---
![Image](https://github.com/user-attachments/assets/7d7d75ce-9677-41d4-82c1-a0b8d7b74af7)
<br>

### 실제 업무에서 사용
---
is를 사용하여 인터페이스를 구현하는지 확인하고, 변환 후 Speak() 메서드를 호출합니다. as는 명확한 다운캐스팅이 필요할 때 사용됩니다.
```c#
using System;

interface IAnimal
{
    void Speak();
}

class Dog : IAnimal
{
    public void Speak() => Console.WriteLine("멍멍!");
}

class Program
{
    static void MakeSound(object obj)
    {
        if (obj is IAnimal animal)
        {
            animal.Speak();
        }
        else
        {
            Console.WriteLine("이 객체는 동물이 아닙니다.");
        }
    }
    
    static void Main()
    {
        object myDog = new Dog();
        MakeSound(myDog);  // 멍멍!
        MakeSound("Not an animal");  // 이 객체는 동물이 아닙니다.
    }
}
```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}