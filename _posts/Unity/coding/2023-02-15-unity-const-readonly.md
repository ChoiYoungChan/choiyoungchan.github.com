---
title:  "[Unity] 유니티 const readonly차이점과 특징"
excerpt: CSV in Unity

categories:
  - Unity Code
tags:
  - [const, readonly, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-02-15
last_modified_at: 2023-02-15
---

## 개요
---
사용 형태로만 정의 하면 둘 다 변수를 변하지 못하는 변수로 만들어 주는 C#키워드입니다. <br>
간단히 하자면, C++에서 const가 컴파일 상수 런타임 상수 둘다 처리 하는 키워드 였다면, C#에서는 확실하게 두개로 나눈것 이라고 이해하시면 됩니다.
<br>

### 차이점
---
어느쪽이든 나중에 값을 변경할 수 없다 라는 공통점이 있긴 하지만, <br>
컴파일 시 아니면 런타임 시 정수로 취급되는가, 유연성, 사용가능한 곳 등의 차이가 있습니다. <br><br>

### const에 관하여
---
const는 컴파일시 상수로 취급되며, 변수 선언과 동시에 값을 할당하여 초기화 해야 합니다.<br>

* 컴파일 타입의 상수입니다 (컴파일시 const 변수의 값을 가져옵니다)
* 내장자료형 (정수형, 실수형, Enum, String)에 대해서만 사용 할 수 있습니다
* 변수 선언과 동시에 값을 할당 해야합니다.
* 메모리 할당 위치는 Stack Memory 이다. 단, static 선언을 하면 Heap Memory에 저장 가능합니다.

<br>

### readonly에 관하여
---
readonly는 모든 자료형에 사용 할 수 있으며, 런타임에 이루어지므로 반드시 생성과 동시에 초기화 할 필요는 없습니다.<br>
단, 생성자 단계에서 단 1번 할당을 통해 초기화 할 수 있습니다.<br>

* 런타임 상수입니다. (exe 또는 dll을 사용할 때 변수의 값을 가져옵니다.)
* 모든 자료형에 사용 할 수 있으며, 생성과 동시에 초기화 할 필요는 없습니다.
* 단, 생성자 단계에서 단 1번 할당을 통해 초기화 할 수 있습니다. 
* 메모리 할당 위치는 Heap Memory입니다.
<br>
<br>


## 사용법
---

```c#
public class Example : MonoBehaviour
{
    // Define a const variable that cannot be changed at runtime
    private const float PI = 3.14f;

    // Define a readOnly variable that can be changed at runtime
    private readonly float speed = 5f;

    private void Start()
    {
        // Attempting to change a const variable will result in a compile error
        // PI = 3.14159f;

        // Changing the value of a readOnly variable at runtime is allowed
        speed = 10f;
    }
}
```



<br>
[Top](#){: .btn .btn--primary }{: .align-right}