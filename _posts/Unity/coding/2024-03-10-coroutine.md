---
title:  "[Unity] 코루틴에 대하여"
excerpt: Coroutine in Unity

categories:
  - Unity Code
tags:
  - [DoTween, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2024-03-10
last_modified_at: 2024-03-10
---

## 개요
---
코루틴은 함수 실행을 일시 중지하고 나중에 다시 재개할 수 있도록 하는 기능입니다. 일반적인 함수는 실행이 시작되면 완료될 때까지 실행되지만, 코루틴은 특정 조건(예: 시간 경과, 프레임 전환)에 따라 실행을 일시 중지하고, 조건이 충족되면 중단된 지점부터 다시 실행을 이어갈 수 있습니다. <br>마치 여러 작업을 번갈아 가며 처리하는 것과 같습니다. 예를 들어, 책을 읽다가 잠시 멈추고 다른 일을 하다가 다시 책을 펴서 읽던 부분을 읽는 것과 비슷합니다.<br><br>

Unity에서 코루틴은 주로 시간 지연, 애니메이션, 비동기 작업 등을 처리하는 데 사용됩니다.
<br><br>

### 특징
---
* 비동기적 실행: 코루틴은 메인 스레드와 별개로 실행되므로, 게임의 성능에 영향을 주지 않고 긴 작업을 처리할 수 있습니다. 하지만, 엄밀히 말하면 멀티 스레딩이 아닌 단일 스레드 내에서 작동합니다.
* yield 문 사용: yield 문을 사용하여 코루틴의 실행을 일시 중지하고 제어권을 Unity 엔진에 반환합니다.
* IEnumerator 반환 타입: 코루틴 함수는 IEnumerator 인터페이스를 반환해야 합니다.

### 작동방식
---
코루틴은 다음과 같은 방식으로 작동합니다.

1. ```StartCoroutine()```함수를 사용하여 코루틴을 시작합니다.
2. 코루틴 함수가 실행되다가 yield 문을 만나면 실행을 일시 중지하고 제어권을 Unity 엔진에 반환합니다.
3. Unity 엔진은 다음 프레임 또는 지정된 시간이 지난 후 코루틴의 실행을 다시 시작합니다.
4. 코루틴 함수가 완전히 실행될 때까지 2-3단계를 반복합니다.

<br><br>

### yield 문의 종류
---
* 

## 주의점
---
코루틴에서 사용되는 주요 yield 문은 다음과 같습니다.

* ```yield return null;```: 다음 프레임까지 대기합니다. 가장 일반적으로 사용되는 yield 문입니다.
* ```yield return new WaitForSeconds(float seconds);```: 지정된 시간(초) 동안 대기합니다.
* ```yield return new WaitForFixedUpdate();```: 다음 FixedUpdate()까지 대기합니다. 물리 연산과 관련된 작업을 처리할 때 유용합니다.
* ```yield return new WaitUntil(Func<bool> predicate);```: 특정 조건이 참이 될 때까지 대기합니다.
* ```yield return new WaitWhile(Func<bool> predicate);```: 특정 조건이 거짓이 될 때까지 대기합니다.
* ```yield return StartCoroutine(Coroutine);```: 다른 코루틴이 완료될 때까지 대기합니다.

<br><br>

### 장단점
---
#### 장점
* 비동기적인 작업 처리 용이: 코루틴을 사용하면 긴 시간이 걸리는 작업이나 특정 시간 간격으로 반복해야 하는 작업을 비동기적으로 처리할 수 있습니다. 이는 게임의 메인 스레드를 막지 않으므로 게임의 부드러운 실행을 유지하는 데 도움이 됩니다. 예를 들어, 네트워크 통신, 파일 입출력, 복잡한 계산 등을 코루틴으로 처리하면 게임이 멈추지 않고 계속 실행될 수 있습니다.
* 간단한 시간 지연 및 애니메이션 구현: ```yield return new WaitForSeconds()```를 사용하면 쉽게 시간 지연을 구현할 수 있으며, 이를 활용하여 애니메이션, 효과, 이벤트 등을 간편하게 처리할 수 있습니다. 예를 들어, 폭발 효과 후 잠시 후 오브젝트를 삭제하거나, 특정 시간 간격으로 오브젝트의 색상을 변경하는 등의 작업을 간단하게 구현할 수 있습니다.
* 코드의 가독성 향상: 여러 프레임에 걸쳐 실행되는 작업을 코루틴으로 표현하면 코드를 훨씬 직관적이고 가독성 좋게 작성할 수 있습니다. 예를 들어, 오브젝트가 특정 경로를 따라 이동하는 작업을 코루틴으로 구현하면 마치 애니메이션처럼 코드를 작성할 수 있어 이해하기 쉽습니다.
* 상태 관리 용이: 코루틴을 사용하면 함수의 실행 상태를 yield 문을 통해 쉽게 관리할 수 있습니다. 이는 복잡한 로직을 여러 단계로 나누어 처리할 때 유용합니다. 예를 들어, 게임의 튜토리얼 단계를 코루틴으로 구현하면 각 단계의 진행 상황을 명확하게 관리할 수 있습니다.

#### 단점 
* 가비지 발생: ```yield return new WaitForSeconds()```와 같은 구문을 반복적으로 사용하면 가비지가 발생할 수 있습니다. 특히 빈번하게 호출되는 코루틴의 경우 성능 저하의 원인이 될 수 있습니다. 이는 마치 일회용품을 계속 사용하는 것과 같습니다. 해결 방법으로는 ```WaitForSeconds``` 객체를 미리 생성해두고 재사용하는 방법이 있습니다.
* 디버깅의 어려움: 코루틴은 일반적인 함수 호출과는 다른 방식으로 실행되기 때문에 디버깅이 다소 어려울 수 있습니다. 실행 흐름을 추적하기 어렵고, 예외 발생 시 원인을 파악하기 어려울 수 있습니다. 마치 미로 속에서 길을 찾는 것과 같습니다.
* 동시성 문제 (제한적인 의미): 유니티의 코루틴은 엄밀히 말하면 멀티 스레딩이 아닌 단일 스레드 내에서 작동합니다. 즉, 진정한 의미의 동시 실행은 불가능하며, 여러 작업을 번갈아 가며 처리하는 방식입니다. 따라서 CPU 집약적인 작업을 코루틴으로 처리하면 메인 스레드의 성능에 영향을 줄 수 있습니다. 마치 한 사람이 여러 가지 일을 번갈아 가며 하는 것과 같습니다.
* 중첩된 코루틴 관리의 어려움: 여러 개의 코루틴을 중첩해서 사용하면 코드의 흐름을 파악하기 어려워지고, 관리가 복잡해질 수 있습니다. 마치 여러 개의 실타래가 엉켜있는 것과 같습니다.

<br>

## 사용법
---

[시간 지연 후 메시지 출력]
```c#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(PrintMessageAfterDelay(3f, "3초 후 메시지 출력!"));
    }

    IEnumerator PrintMessageAfterDelay(float delay, string message)
    {
        yield return new WaitForSeconds(delay);
        Debug.Log(message);
    }
}
```
<br>

[프레임 단위로 오브젝트 이동]
```c#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    public Transform target;
    public float speed = 1f;

    void Start()
    {
        StartCoroutine(MoveTowardsTarget());
    }

    IEnumerator MoveTowardsTarget()
    {
        while (transform.position != target.position)
        {
            transform.position = Vector3.MoveTowards(transform.position, target.position, speed * Time.deltaTime);
            yield return null; // 다음 프레임까지 대기
        }
    }
}
```
<br>

[비동기 작업 시뮬레이션]
```c#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(SimulateAsyncOperation());
    }

    IEnumerator SimulateAsyncOperation()
    {
        Debug.Log("비동기 작업 시작...");
        yield return new WaitForSeconds(2f); // 2초 동안 작업 시뮬레이션
        Debug.Log("비동기 작업 완료!");
    }
}
```


<br>

[Top](#){: .btn .btn--primary }{: .align-right}