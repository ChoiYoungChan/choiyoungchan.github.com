---
title: "[C#] C#의 Substring사용법과 설명 완벽 정리 (C# 예시 코드 포함)"
excerpt: Substring

categories:
  - C Sharp
tags:
  - [C#, Substring, 서브스트링, C# 문법]

toc: true
toc_sticky: true
 
date: 2024-09-07
last_modified_at: 2024-09-07
---

## 개요
---
```Substring```은 C#의 string 클래스에서 제공하는 메서드로, 문자열의 지정된 위치에서 시작하여 지정된 길이만큼의 부분 문자열을 반환합니다. 원본 문자열은 변경되지 않고, 새로운 문자열 객체가 생성되어 반환됩니다.<br> 
예를들자면 긴 빵에서 원하는 부분만 잘라내는 것과 같은 원리라고 생각하면 이해하기 쉬우실 겁니다.
<br><br>

### Substring 메서드의 두 가지 형태
---
```Substring``` 메서드는 두 가지 형태를 가지고 있습니다.

* ```Substring(int startIndex)```: 지정된 ```startIndex```부터 문자열의 끝까지 부분 문자열을 반환합니다.
* ```Substring(int startIndex, int length)```: 지정된 ```startIndex```에서 시작하여 length만큼의 부분 문자열을 반환합니다.
<br><br>

### Substring의 활용
---
```Substring```은 다양한 상황에서 유용하게 사용될 수 있습니다.

* 문자열 파싱: 특정 형식의 문자열에서 필요한 데이터 추출 (예: 날짜, 시간, 파일 경로 등)
* 데이터 전처리: 텍스트 데이터에서 불필요한 부분 제거 또는 원하는 부분만 추출
* UI 프로그래밍: 텍스트 박스 등에서 입력된 텍스트의 일부분을 처리
* 파일 이름 또는 경로 처리: 파일 이름에서 확장자 분리, 경로에서 폴더 이름 추출 등

<br>

### Java의 substring과의 차이점
---
Java의 ```substring``` 메서드와 C#의 ```Substring``` 메서드는 유사하지만, 미묘한 차이점이 있습니다. ```Java의 substring(beginIndex, endIndex)```는 ```beginIndex```부터 ```endIndex - 1```까지의 문자열을 반환하는 반면, C#의 ```Substring(startIndex, length)```는 ```startIndex```부터 length개의 문자를 반환합니다. 즉, Java는 끝 인덱스를 exclusive로 취급하고, C#은 길이로 취급합니다. 이 차이점을 명확히 이해하고 사용해야 합니다.

<br>

## 예시 코드
---
```c#
using System;

public class SubstringExample
{
    public static void Main(string[] args)
    {
        string str = "Hello, C# Programming!";

        // Substring(int startIndex) 사용 예시
        string sub1 = str.Substring(7); // 인덱스 7부터 끝까지 추출
        Console.WriteLine(sub1); // 출력: C# Programming!

        // Substring(int startIndex, int length) 사용 예시
        string sub2 = str.Substring(0, 5); // 인덱스 0부터 5개의 문자 추출
        Console.WriteLine(sub2); // 출력: Hello

        string sub3 = str.Substring(7, 2); // 인덱스 7부터 2개의 문자 추출
        Console.WriteLine(sub3); // 출력: C#

        // startIndex가 문자열 길이보다 크거나 음수인 경우 ArgumentOutOfRangeException 발생
        try
        {
            string sub4 = str.Substring(str.Length); // 문자열 길이와 같은 index를 넣으면 에러 발생
            Console.WriteLine(sub4);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine($"Error: {e.Message}"); // 출력: Index and length must refer to a location within the string.
        }

        try
        {
            string sub5 = str.Substring(-1); // 음수 index를 넣으면 에러 발생
            Console.WriteLine(sub5);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine($"Error: {e.Message}"); // 출력: Index and length must refer to a location within the string.
        }

        // length가 startIndex 이후 남은 문자열 길이보다 큰 경우 ArgumentOutOfRangeException 발생
        try
        {
            string sub6 = str.Substring(7, 20); // startIndex 이후 남은 문자열 길이보다 큰 length를 넣으면 에러 발생
            Console.WriteLine(sub6);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine($"Error: {e.Message}"); // 출력: Index and length must refer to a location within the string.
        }
    }
}
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}