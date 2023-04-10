---
title:  "[C++] 전처리기 preprocesser"
excerpt: preprocesser in c++

categories:
  - Cpp
tags:
  - [Cpp, C++, preprocesser, 전처리기]

toc: true
toc_sticky: true
 
date: 2022-12-01
last_modified_at: 2022-12-01
---

## 전처리기이란?
---
전처리기(preprocessor)는 프로그램을 컴파일할 때 컴파일 직전에 실행되는 별도의 프로그램입니다. <br>
전처리기가 실행되면 각 코드 파일에서 지시자(directives)를 찾고, 지시자(directives)는 #으로 시작해서 줄 바꿈으로 끝나는 코드입니다. <br>
(대표적으로 ``` #include ```,  ```#define```,  ```#region``` 그리고 조건부 컴파일 등이 있습니다.) <br>
<br>


### 예제
---

#include<br>
컴파일러와 함께 제공되는 헤더파일은 <>를 이용해서 포함시키고, 따로 사용자가 작성한 헤더파일은 소스코드가 있는 경로 기준으로 해서 ""를 이용해서 포함시킵니다. <br>

```c++
#include <iostream>	// 컴파일러에서 제공되는 헤더파일
#include "MemoryBlock.h" // 사용자 정의 헤더파일
```

주로 사용하는 헤더 파일 <br>
```
<iostream> : C++에서 가장 많이 사용하는 헤더파일로 기본적인 입출력에 관한 기능을 포함합니다.
<string> : 문자열 타입인 std::string관련 함수를 포함하는 헤더파일
<chrono> : 시간 관련 헤더파일
<filesystem> : 파일 시스템 관련 헤더파일
<thread> : 쓰레드 관련 헤드파일
<iomanip> : 입출력 조정자에 관한 헤더파일
<fstream> : 파일 스트림 관련 헤더파일
<vector> : std::vector이 있는 헤더파일
```
<br>

매크로 #define <br>

```c++
#include <iostream>	// 컴파일러에서 제공되는 헤더파일
#include "MemoryBlock.h" // 사용자 정의 헤더파일
```

define에 대한 설명과 예시->[c++ define](https://choiyoungchan.github.io/cpp/define/)

<br>
조건부 컴파일 #ifdef<br>
컴파일을 할 조건을 지정하여 컴파일을 하거나 하지않을 수 있습니다.<br>

```c++
#ifdef 조건
std::cout << "조건부 컴파일" << std::endl;
#endif
```


<br>

[Top](#){: .btn .btn--primary }{: .align-right}