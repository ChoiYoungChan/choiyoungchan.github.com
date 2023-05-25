---
title:  "[C++] 가변 매개 변수"
excerpt: Variable parameters in c++

categories:
  - Cpp
tags:
  - [Cpp, C++, Variable parameters, 가변 매개 변수]

toc: true
toc_sticky: true
 
date: 2022-11-21
last_modified_at: 2022-11-21
---

## 개념
---
파라매터수를 동적으로 넣는 방법에 대해 알아보겠습니다. <br>
실제 현장에서는 잘 사용되지 않는 방법이기 때문에 그냥 이러한 개념이다 라는 정도로만 짚고 넘어가 주셔도 상관없습니다. <br>
(전 지금까지 한번도 못봤습니다.)


## 사용법
---

먼저 아래와 같이 <stdarg.h> 헤더를 사용하기때문에 include해줍니다.<br>
```c++
#include <stdarg.h>
```
상기의 헤더 파일에는 va_start를 포함한 몇몇가지가 정의 되어 있습니다.<br>
가변 매개 변수를 사용하기 위해서는 그중 아래의 기능을 사용합니다.<br>
* va_start
* va_end
* va_arg
<br><br>

가변인자를 가지는 함수는 아래와 같이 매개변수를 고정인자와 가변인자를 넣어야합니다.<br>
가변인자는 '...'으로 표현하며, 고정인자의 뒤에 와야 합니다. <br>
```c++
void AddWidget(int widget_count, ...)
```
<br>

va_list는 가변인자의 주소를 나타내는 포인터 입니다.<br>
va_start(va_list는, 고정인자)는 초기화 작업으로, 고정인자 바로 뒤에 가변인자를 배치하고 va_list에 첫 가변인자의 주소를 할당합니다.<br>
```c++
va_list _va_list;
va_start(_va_list, widget_count);
```
<br>

va_arg(va_list, 자료형)는 va_start로 할당한 va_list의 값(가변인자 값)을 리턴한 후 va_list의 주소를 자료형만큼 뒤로 이동시킵니다. <br>
그렇게되면 다음 가변인자의 주소값이 va_list로 할당되고, 이를 가변인자 개수만큼 반복하여 모든 가변인자들을 출력할 수 있습니다. <br>
```c++
for(int i=0; i<widget_count; i++)
{
    int result_num = va_arg(_va_list, int);
    printf("%d ", result_num);
}
```

마지막으로, va_end();는 va_list를 초기화하는 역할 입니다.
```c++
va_end(_va_list);
```

전체 코드
```c++
#include <stdio.h>
#include <stdarg.h>

void AddWidget(int widget_count, ...)
{
    va_list _va_list;
    va_start(_va_list, widget_count);

    for(int i=0; i<widget_count; i++)
    {
        int result_num = va_arg(_va_list, int);
        printf("%d ", result_num);
    }

    va_end(_va_list);
}

int main()
{
    AddWidget(0, 10); // print : 10
    printf("\n");
    AddWidget(1, 10, 20); // print : 10 20
    printf("\n");
    AddWidget(2, 10, 20, 30); // print : 10 20 30 
}
```


<br>

[Top](#){: .btn .btn--primary }{: .align-right}