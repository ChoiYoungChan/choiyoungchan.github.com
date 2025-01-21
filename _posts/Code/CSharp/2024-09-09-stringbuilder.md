---
title:  "[C#] C#의 StringBuilder사용법과 설명 완벽 정리 (C# 예시 코드 포함)"
excerpt: Attribute : StringBuilder

categories:
  - C Sharp
tags:
  - [C#, StringBuilder, 스트링빌더]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

## 개요
---
C#에서 문자열(string)은 불변(immutable) 객체입니다. 즉, 문자열을 수정하는 모든 작업(예: 문자열 연결, 삽입, 삭제 등)은 새로운 문자열 객체를 생성합니다. 이러한 특성 때문에 문자열을 빈번하게 수정하는 경우, 불필요한 메모리 할당과 해제가 반복되어 성능 저하를 초래할 수 있습니다.<br>

StringBuilder는 이러한 문제를 해결하기 위해 도입된 가변(mutable) 문자열 클래스입니다. StringBuilder 객체는 내부적으로 문자 배열을 사용하여 문자열을 저장하며, 문자열을 수정하는 작업을 효율적으로 수행할 수 있도록 설계되었습니다.
<br><br>

### StringBuilder의 특징
---
* 가변성(Mutability): 문자열을 수정해도 새로운 객체를 생성하지 않고 내부적으로 변경합니다.
* 성능 향상: 문자열을 빈번하게 수정하는 작업에서 string 클래스보다 훨씬 뛰어난 성능을 보입니다.
* 다양한 메서드 제공: 문자열 추가, 삽입, 삭제, 치환 등 다양한 문자열 조작 메서드를 제공합니다.
<br><br>

### StringBuilder의 주요 메서드
---

* ```Append()```: 문자열을 ```StringBuilder```객체 뒤에 추가합니다.
* ```Insert()```: 지정된 위치에 문자열을 삽입합니다.
* ```Remove()```: 지정된 위치에서 지정된 개수의 문자를 삭제합니다.
* ```Replace()```: 특정 문자 또는 문자열을 다른 문자 또는 문자열로 치환합니다.
* ```ToString()```: ```StringBuilder``` 객체의 내용을 string 객체로 변환합니다.

<br>

### StringBuilder의 활용 시점
---
* 반복적인 문자열 수정: 루프 안에서 문자열을 추가, 삽입, 삭제하는 경우
* 많은 문자열 연결: 여러 개의 문자열을 하나로 연결하는 경우
* 문자열 포맷팅: 복잡한 문자열 형식을 만드는 경우
<br><br>

## 예시 코드
---

```c#
using System;
using System.Text; // StringBuilder를 사용하기 위해 추가

public class StringBuilderExample
{
    public static void Main(string[] args)
    {
        // StringBuilder 객체 생성
        StringBuilder sb = new StringBuilder("Hello");

        // Append() 메서드: 문자열 추가
        sb.Append(", World!");
        Console.WriteLine(sb.ToString()); // 출력: Hello, World!

        // Insert() 메서드: 문자열 삽입
        sb.Insert(5, " C#");
        Console.WriteLine(sb.ToString()); // 출력: Hello C#, World!

        // Remove() 메서드: 문자열 삭제
        sb.Remove(5, 3); // " C#" 삭제
        Console.WriteLine(sb.ToString()); // 출력: Hello, World!

        // Replace() 메서드: 문자열 치환
        sb.Replace("World", "C# Programming");
        Console.WriteLine(sb.ToString()); // 출력: Hello, C# Programming!

        // 여러 줄의 문자열 추가
        sb.AppendLine(); // 새 줄 추가
        sb.AppendLine("This is a new line.");
        Console.WriteLine(sb.ToString());
        /* 출력:
        Hello, C# Programming!
        
        This is a new line.
        */

        // 초기 용량 설정
        StringBuilder sbWithCapacity = new StringBuilder(100); // 초기 용량을 100으로 설정
        Console.WriteLine($"Capacity: {sbWithCapacity.Capacity}"); // 출력: Capacity: 100

        // 최대 용량 설정
        StringBuilder sbWithMaxCapacity = new StringBuilder(10, 50); // 초기 용량 10, 최대 용량 50으로 설정
        Console.WriteLine($"MaxCapacity: {sbWithMaxCapacity.MaxCapacity}"); // 출력: MaxCapacity: 50
    }
}
```
<br>

### string과 StringBuilder의 성능 비교
---

```c#
using System;
using System.Diagnostics; // Stopwatch를 사용하기 위해 추가
using System.Text;

public class PerformanceComparison
{
    public static void Main(string[] args)
    {
        int iterations = 10000;
        string str = "";
        StringBuilder sb = new StringBuilder();

        // string을 사용한 문자열 연결 시간 측정
        Stopwatch sw = Stopwatch.StartNew();
        for (int i = 0; i < iterations; i++)
        {
            str += "a";
        }
        sw.Stop();
        Console.WriteLine($"string concatenation: {sw.ElapsedMilliseconds}ms");

        // StringBuilder를 사용한 문자열 연결 시간 측정
        sw.Restart();
        for (int i = 0; i < iterations; i++)
        {
            sb.Append("a");
        }
        sw.Stop();
        Console.WriteLine($"StringBuilder append: {sw.ElapsedMilliseconds}ms");
    }
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}