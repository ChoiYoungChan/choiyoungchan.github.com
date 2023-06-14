---
title:  "[C++] C++에서 사용하는 전방선언, 전방정의"
excerpt: forward declaration and definitions in C++

categories:
  - Cpp
tags:
  - [C++, forward declaration, forward definitions, 전방선언, 전방정의]

toc: true
toc_sticky: true
 
date: 2023-01-02
last_modified_at: 2023-01-02
---

## 개념
--- 

먼저 아래의 예시 코드를 읽어주세요. <br>

```c++
#include <iostream>

int main()
{
    std::cout << "The sum of 1 and 2 is: " << Add(1, 2) << std::endl;

    return 0;
}

int Add(int x, int y)
{
    return x + y;
}
```

<br>
이제 C++를 입문하신 분들은 아마 결과를 아래와 같이 생각하실 겁니다만,  <br>
이는 잘못되었습니다. <br>

```
The sum of 1 and 2 is: 3
```

<br>
결과값은 아래와 같이 컴파일 에러가 발생합니다.<br>

```
error C3861: 'Add': 식별자를 찾을 수 없습니다.
```

<br>
상기의 에러가 발생하는 이유는 컴파일러가 프로그램을 순차적으로 읽기 때문 입니다. <br>
컴파일러가 main()함수내 5번째 행의 Add함수를 호출시 9행까지 Add함수를 정의하지 않았으므로 Add함수가 무엇인지 알 수 없습니다. <br>
따라서 상기와 같이 식별자를 찾을 수 없음 이라는 에러가 발생합니다. <br>
<br>
 
```c++
#include <iostream>

int Add(int x, int y)
{
    return x + y;
}

int main()
{
    std::cout << "The sum of 1 and 2 is: " << Add(1, 2) << std::endl;

    return 0;
}
```

<br>
때문에 상기와 같은 방법으로 main함수가 Add함수를 호출 할 때 컴파일러는 Add함수가 무엇인지 알 수 있습니다.  <br>
상기의 프로그램은 간단하므로 변경이 쉽지만, 실무 에서는 더 크고 복잡한 프로그램이기 때문에 어떤 함수가 다른 함수를 어떤 순서로 호출하는지 파악하는것은 매우 복잡합니다. <br>
<br>


## 전방선언
--- 
전방선언(forward declaration)은 식별자를 정의하기 전에 식별자의 존재를 컴파일러에 미리 알려주는것 입니다.<br>

함수의 경우, 함수의 몸체를 정의 하기 전에 함수의 존재에 대해 미리 알리는것을 말하며, <br> 
이 방법으로 컴파일러가 함수를 호출할 때 함수가 정의된 방법이나 위치를 아직 모를 때 에도 함수를 호출한다는것 을 이해시킬 수 있습니다.<br>

함수의 전방 선언을 하려면 아래와 같이 함수 원형이라고 하는 선언문을 사용해야 합니다.<br>
함수 원형은 리턴타입, 이름, 매개 변수로 구성, 세미콜론으로 끝나게되고 몸체는 포함하지 않습니다.<br>


```c++
int Add(int num_1, int num_2);
```
<br>

또한 함수 원형에서 매개 변수의 이름을 지정하지 않고도 선언을 할 수 있지만, 실제 함수 매개 변수가 무엇인지는 파악하기 위해서는 가급적 매개변수 이름을 지정하는것이 좋습니다. <br>

여기서 함수 매개변수가 무엇인지는 파악하는게 왜 중요하느냐하면, <br>
실무에서는 개인 개발 형식도 많이 있습니다만 일정 규모의 프로젝트 이상은 최소 5명, 20~100명이나 어쩌면 그 이상의 프로그래머가 협업 하는 방식이기 때문입니다. <br>

즉, 가독성의 문제인데, 프로그래머 특성상 제가 작성한 코드를 다른 사람이 수정 또는 개선할수도, 다른사람의 코드를 제가 수정할 수도 있어야 하는게 일반적이고 실제로도 그러한 일이 많이 있습니다. <br><br>
매개 변수가 무엇인지는 함수 이름과 파일의 위치, 사용처, 내용, 디버깅 등을 해보면 알기야 하겠지만 가급적 그런것을 파악할 시간도 줄여야만 하는게 업무상으로도, 평가적으로도 좋기 때문 입니다.<br>

```c++
int Add(int num_1, int num_2);
```
<br>


아래는 처음의 예시 코드를 함수 원형을 사용하여 동작 하도록 한 코드 입니다.
```c++
#include <iostream>

int Add(int num_1, int num_2);

int main()
{
    std::cout << "The sum of 1 and 2 is: " << Add(1, 2) << std::endl;

    return 0;
}

int Add(int x, int y)
{
    return x + y;
}
```

<br> 

### 선언, 정의 차이점
--- 

선언 : 식별자(변수 또는 함수)를 실제로 구현하거나 메모리 할당(인스턴스화) 하는것 <br>
정의 : 식별자 및 해당 타입의 존재를 컴파일러에게 알려주는 명령문 <br>
<br>

```c++
int Add(int x, int y) // Add() 함수를 정의(구현)
{
    return x + y;
}

int game_money; // game_money라는 정수형 변수를 메모리 할당(인스턴스화)
```

<br>

```c++
// 컴파일러에게 두 개의 int 매개 변수를 사용하고 int를 반환하는 "Add"라는 이름의 함수를 알려준다.
int Add(int num_1, int num_2);

int game_money; // game_money라는 정수형 변수를 컴파일러에게 알려준다.
```


<br>
[Top](#){: .btn .btn--primary }{: .align-right}