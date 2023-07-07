---
title:  "[C#] string 포맷"
excerpt: string format in C#

categories:
  - C Sharp
tags:
  - [C#, string format, string 포맷, 문자열 포맷]

toc: true
toc_sticky: true
 
date: 2023-07-07
last_modified_at: 2023-07-07
---

## 개념
--- 
### 문자열 포맷(string format) <br>
string.Format() 메서드는 말 그대로 문자열을 지정된 형식으로 포맷 하는데 사용됩니다. 
예를 들어, 다음과 같은 코드는 “Hello, {0}!” 에서 {0}이라는 식별자를 “John Doe”라는 문자열로 포맷 합니다.<br> <br>

```c#
string formattedString = string.Format(“Hello, {0}!“, “John Doe”);
```
 <br>
프로그래밍을 배우기 시작할때 기본적으로 Print에서 인자를 넣어 출력하는것을 배우는데 이것과 비슷하게 문자열을 포맷할 때 {0}, {1}, {2}와 같은 식별자를 사용하여 문자열의 위치를 나타냅니다(첫번째 인자는 {0}, 두번째는 {1}, 세번째는 {2}입니다. 당연히 네번째부터는 {3}... 이겠죠?)<br>

<br>

## 예제
--- 

```c#
string formattedString = string.Format("Hello, {0}!", "John Doe");
```
<br>

출력
```
Hello, John Doe!
```
<br>

인자가 여러개
```c#
string formattedString = string.Format("{0} is {1} years old, born in{2} ", "John Doe", "25", "1993");

```
<br>

출력
```
John Doe is 25 years old, born in 1993
```
<br>

이는 실제로 게임 내에서도 사용할 수 있습니다.<br>
텍스트에 아래와 같이 {0}/{1} 포맷으로 정하고 코드 상에서 이를 string.Format으로 읽은 후, 각각의 변수를 가져와 읽어들인 포맷 형식내에 각각의 식별자에 넣어주는 식으로 적용이 가능합니다.<br><br>

![string_format_00](https://github.com/ChoiYoungChan/choiyoungchan.github.com/assets/40765022/140f99e1-4dce-452f-a83b-4381559457ed)<br><br>

```c#
_clearText = transform.Find("stage_header_text").GetComponent<Text>();
_formatText = _clearText.text;
.
.
.
_clearText.text = string.Format(_formatText, clearStageCount, allStageCount);
```
<br>

결과<br>

![string_format_01](https://github.com/ChoiYoungChan/choiyoungchan.github.com/assets/40765022/edbb8592-7214-498e-a9d2-6495cc96037a)
<br>




<br>
[Top](#){: .btn .btn--primary }{: .align-right}