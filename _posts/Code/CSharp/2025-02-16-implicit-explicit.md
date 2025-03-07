---
title:  "[C#] implicit(암시적 변환) 과 explicit(명시적 변환) 핵심 정리 + C# 샘플 코드"
excerpt: implicit and explicit

categories:
  - C Sharp
tags:
  - [C#, implicit, explicit, 암시적 변환, 명시적 변환]

toc: true
toc_sticky: true
 
date: 2025-02-16
last_modified_at: 2025-02-16
---

## implicit(암시적 변환) 과 explicit(명시적 변환)
---
C#에서 implicit(암시적 변환) 과 explicit(명시적 변환) 은 사용자 정의 타입 변환을 구현할 때 사용됩니다.
이 개념을 정확히 이해하면 사용자 정의 클래스를 보다 안전하고 직관적으로 변환할 수 있습니다.
<br><br>

![Image](https://github.com/user-attachments/assets/6f2016f7-63ee-4a3a-956d-a7b89c95b757)
<br><br>

✔ 예제: 기본형 변환
```c#
int x = 10;
double y = x;  // 암시적 변환 (int → double)

double a = 9.7;
int b = (int)a;  // 명시적 변환 (double → int, 소수점 손실 발생)
```
위 코드에서 int → double 변환은 데이터 손실이 없으므로 자동(implicit) 변환되지만,
double → int 변환은 소수점이 손실될 수 있어 명시적(explicit) 변환이 필요합니다. 
<br><br>

### 사용자 정의 타입에서 implicit 변환
---
암시적 변환(implicit) 은 데이터 손실 없이 안전한 경우 사용됩니다.
이 경우, 명시적 캐스트 없이 자연스럽게 변환할 수 있습니다.<br><br>

✔ 예제: Dollar → Euro 변환 (안전한 변환)
```c#
using System;

class Dollar
{
    public double Amount { get; }

    public Dollar(double amount)
    {
        Amount = amount;
    }

    // 암시적 변환: Dollar → Euro (1 Dollar = 0.9 Euro)
    public static implicit operator Euro(Dollar d)
    {
        return new Euro(d.Amount * 0.9);
    }
}

class Euro
{
    public double Amount { get; }

    public Euro(double amount)
    {
        Amount = amount;
    }

    public override string ToString()
    {
        return $"{Amount} EUR";
    }
}

class Program
{
    static void Main()
    {
        Dollar usd = new Dollar(10);  
        Euro eur = usd;  // 암시적 변환 (캐스트 연산자 필요 없음)
        
        Console.WriteLine(eur);  // "9 EUR"
    }
}
```
✔ Dollar → Euro 변환은 데이터 손실이 없으므로 implicit 변환을 사용했습니다.<br>
✔ usd 객체를 Euro로 변환할 때 명시적인 (Euro)usd 캐스트 없이 자동 변환 됩니다.
<br><br>

### 사용자 정의 타입에서 explicit 변환
---
명시적 변환(explicit) 은 데이터 손실이 발생할 가능성이 있거나 의미적 차이가 있는 경우 사용됩니다.
이 경우, 캐스트 연산자가 반드시 필요 합니다.<br><br>

✔ 예제: Kilometer → Meter 변환 (단위 차이 있음)
```c#
using System;

class Kilometer
{
    public double Value { get; }

    public Kilometer(double km)
    {
        Value = km;
    }

    // 명시적 변환: Kilometer → Meter (1 km = 1000 m)
    public static explicit operator Meter(Kilometer km)
    {
        return new Meter(km.Value * 1000);
    }
}

class Meter
{
    public double Value { get; }

    public Meter(double m)
    {
        Value = m;
    }

    public override string ToString()
    {
        return $"{Value} m";
    }
}

class Program
{
    static void Main()
    {
        Kilometer km = new Kilometer(3);  
        // Meter m = km;  // ❌ 오류 발생 (암시적 변환 불가능)
        Meter m = (Meter)km;  // ✅ 명시적 캐스트 필요

        Console.WriteLine(m);  // "3000 m"
    }
}
```
✔ Kilometer → Meter 변환은 데이터가 커질 수 있기 때문에 명시적 변환이 필요합니다.<br>
✔ (Meter)km 와 같이 명시적으로 캐스트 연산자를 사용해야 변환 가능 합니다.
<br><br>

### implicit vs explicit 비교
---
![Image](https://github.com/user-attachments/assets/1e95557b-f356-4a58-af64-23b7af7189e3)
<br><br>

### 주의할 점
---
✅ 암시적 변환이 너무 남발되면 원치 않는 변환이 발생할 수 있음<br>
✅ 명시적 변환을 무조건 강요하면 코드가 복잡해질 수 있음<br>
✅ 변환 연산자를 오버로딩할 때 implicit과 explicit을 적절히 사용해야 유지보수성이 좋아짐
<br><br>

## 정리
---
1️⃣ 암시적 변환(implicit)
* 안전한 변환일 때 사용
* Dollar → Euro 같은 변환에 적합

2️⃣ 명시적 변환(explicit)
* 데이터 손실 가능성이 있는 경우 사용
* double → int, Kilometer → Meter 같은 변환에 적합

3️⃣ implicit과 explicit을 적절히 사용하면 코드의 가독성과 안전성이 높아짐
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}