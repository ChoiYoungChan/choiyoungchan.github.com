---
title:  "[C++] Atoi함수 구현"

categories:
  - Cpp
tags:
  - [Programming, c++, Atoi, Cpp]

toc: true
toc_sticky: true
 
date: 2022-08-08
last_modified_at: 2022-08-08
---

## Atoi의 개념
---
<br>

* 문자열을 정수로 변환한다.
* 문자열 초반의 공백은 무시한다.(아스키 코드로는 9~13, ''는 아스키 코드로 32)
* (+) 또는 (-) 부호는 최대 1개 까지만 올 수 있다.
* 숫자를 읽기 시작해서 다른 문자가 나오기 직전까지만 숫자를 읽는다.

<br>

## 코드 및 주석
---

[선언 및 main]

```c++
int main()
{
    char *text = new char[10];
    
    // input text data to char
    printf("input number text : ");
    scanf_s("%s" , text, 10);

    // output Atoi result
    printf("output Atoi result : %d", Atoi(text));
}
```
 <br>

[Atoi 함수 정의]

```c++
/// <summary>
/// Define Atoi function
/// </summary>
/// <param name="_text_data">input char text data</param>
/// <returns></returns>
int Atoi(char* _text_data) {
    int result = 0, positive = 1;

    // check whitespace
    while ((*_text_data == ' ') || (*_text_data == '\n') || (9 <= *_text_data && *_text_data <= 13))
        _text_data++;

    // check + or -
    if (*_text_data == '+' || *_text_data == '-') {
        if (*_text_data == '-')
            positive = -1;
        _text_data++;
    }

    // change text data to int data
    while ('0' <= *_text_data && *_text_data <= '9') {
        // _data * 10 is make number of digits
        result *= 10;
        // reason why doing [ - '0' ], 
        // cuz input text data is entered as an ASCII code value,
        // so, you can get input number through subtract 0(ASCII value 48)
        result += (*_text_data - '0') * positive;
        _text_data++;
    }
    return result;
}
```
<br>

[전체 코드]

```c++
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>

// declaration Atoi function
int Atoi(char *);

int main()
{
    char *text = new char[10];
    
    // input text data to char
    printf("input number text : ");
    scanf_s("%s" , text, 10);

    // output Atoi result
    printf("output Atoi result : %d", Atoi(text));
}

/// <summary>
/// Define Atoi function
/// </summary>
/// <param name="_text_data">input char text data</param>
/// <returns></returns>
int Atoi(char* _text_data) {
    int result = 0, positive = 1;

    // check whitespace
    while ((*_text_data == ' ') || (*_text_data == '\n') || (9 <= *_text_data && *_text_data <= 13))
        _text_data++;

    // check + or -
    if (*_text_data == '+' || *_text_data == '-') {
        if (*_text_data == '-')
            positive = -1;
        _text_data++;
    }

    // change text data to int data
    while ('0' <= *_text_data && *_text_data <= '9') {
        // _data * 10 is make number of digits
        result *= 10;
        // reason why doing [ - '0' ], 
        // cuz input text data is entered as an ASCII code value,
        // so, you can get input number through subtract 0(ASCII value 48)
        result += (*_text_data - '0') * positive;
        _text_data++;
    }
    return result;
}
```

<br>

## 실행 결과
---
### 부호를 붙이지 않으면
---
![atoi_02](https://user-images.githubusercontent.com/40765022/183655415-9292426b-85e0-4f5a-8a85-b8de01a3104e.png)

양수로 취급하여 출력 <br><br>

---

### - 부호 추가
---
![atoi_03](https://user-images.githubusercontent.com/40765022/183655481-86186eb4-456a-4023-b893-16bd89c724e0.png)


<br>

[Top](#){: .btn .btn--primary }{: .align-right}