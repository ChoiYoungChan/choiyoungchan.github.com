---
title:  "[C++] static_assert란?"
excerpt: static_assert in C++

categories:
  - Cpp
tags:
  - [Programming, c++, static_assert, Cpp]

toc: true
toc_sticky: true
 
date: 2023-04-08
last_modified_at: 2023-04-08
---

## static_assert의 개념
---
<br>
static_assert는 C++11에 추가된 키워드로, 인자로 전달된 식의 참/거짓을 컴파일 타임에 확인합니다. <br>

static_assert에 전달된 식이 참이라면 컴파일러에 의해 해당 식은 무시되고, 거짓이라면 해당 식에서 컴파일 에러를 발생시킵니다. <br>
 <br>
주로 템플릿 메타 프로그래밍에서 사용되며, 당연하게도 프로그램의 안정성과 유효성을 확보하기 위해 사용됩니다. <br>



## 코드 및 설명
---

[static_assert의 형태]

```c++
static_assert(constant_expression, "assert error message");
static_assert(constant_expression); // (에러 메시지는 생략할 수 있습니다.)
```
<br>

여기서 ```constant_expression``` 는 컴파일 타임에 결정되는 상수인데 이 값이 false일 경우,<br>
해당 매크로가 호출된 위치에서 ```assert error message``` 라는 에러 메시지를 나타내며 컴파일 에러를 발생시킵니다. <br>


[간단한 예시] <br>
아래의 코드에서 print는 정수형 타입만 받을 수 있게 std::is_integral타입 특성을 이요해
조건 검사를 수행하고 있습니다. <br>
```print("static_assert");``` 와 같이 정수형이 아닌 타입일 경우 static_assert구문이 실패하여 컴파일 오류가 발생하고 ```print() requires an integral type.``` 에러 메시지가 출력됩니다.  <br>

```c++
#include <iostream>
#include <type_traits>

template <typename T>
void print(T type) {
	std::cout << type << std::endl;
	static_assert(std::is_integral<T>::value, "print() requires an integral type.");
}

void main() {
	print(10);
	print("static_assert"); // static_assert will trigger here
}
```
<br>

[잘못된 사용법] <br>

다만 아래와 같이 static_assert의 조건 검사에서 항상 ```true``` 가 반환되는 상수 표현식은 사용할 수 없습니다. <br>

```c++
#include <iostream>
#include <type_traits>

int main() {
  static_assert(1 == 0, "error message"); // error
  return 0;
}
```

<br>

## 실행 결과
---


<br>

[Top](#){: .btn .btn--primary }{: .align-right}

