---
title:  "[C#] C#에서 문자열 길이 구하는 함수 구현"
excerpt: Implementing function that obtains string length from C#

categories:
  - C Sharp
tags:
  - [Programming, C#, Strlen, C Sharp]

toc: true
toc_sticky: true
 
date: 2023-02-14
last_modified_at: 2023-02-14
---

## Strlen의 개념
---
<br>
이전에 C++에서 문자열 길이를 구하는 Strlen함수를 구현 했었습니다.<br>
당연하지만 C#에도 문자열 길이를 구할 수 있습니다. <br>
차이점이 있다면 C, C++와는 달리 Strlen함수를 사용하는것이 아닌 string.Length 프로퍼티를 사용한다는 부분입니다. <br><br>

string.Length 프로퍼티에 대해 간단히 설명하자면, string.Length 프로퍼티는 해당 문자열의 길이를 반환하는 읽기 전용 프로퍼티이며 문자열에 포함된 문자의 개수를 나타냅니다. <br>
string.Length는 string 클래스의 프로퍼티로서, 인스턴스화된 문자열 객체에 대해 바로 접근할 수 있다는 특징이 있습니다. <br><br>
그래서 오늘은 string.Length 의 간단한 샘플 코드를 보고 바로 string.Length 와 동일하게 문자열 길이를 구하는 함수를 한번 직접 구현해 보겠습니다. <br>
(매우 쉽고 기초적인 부분이니 금방 하실 수 있습니다.)

<br>

## 코드 및 주석
---

[Sample Code]

```c#
string str = "Hello, World!";
int length = str.Length; // 문자열 길이를 구함
Console.WriteLine("The length of the string is: " + length);
```
 <br>

[직접 구현해 보기]

```c#
using System;

namespace test
{
    class MainClass
    {
        public static int StringLength(string input)
        {
            int length = 0;

            foreach (char c in input)
            {
                length++;
            }

            return length;
        }

        public static int Main()
        {
            string _text = "sampleText";
            Console.WriteLine($"Length of the string: {StringLength(_text)}");
            return 0;
        }
    }
}

```

<br>

## 실행 결과
---
<br>

![c#_strlen_000](https://user-images.githubusercontent.com/40765022/232496467-c76a3cff-8274-40f5-b8cf-ad1a4928b81b.png)

<br>

[Top](#){: .btn .btn--primary }{: .align-right}