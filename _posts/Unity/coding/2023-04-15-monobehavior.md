---
title:  "[Unity] 유니티에서 Monobehavior"
excerpt: Monobehavior in Unity

categories:
  - Unity Code
tags:
  - [Monobehavior, 모노비헤이비어, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-04-15
last_modified_at: 2023-04-15
---

## 개요
---
MonoBehaviour는 유니티에서 스크립트를 만들기 위한 기본 클래스입니다. <br>
게임 오브젝트에 부착되어 게임 오브젝트의 동작을 정의하고 제어하는 역할을 합니다. <br>
즉, 게임 오브젝트에게 생명을 불어넣어주는 핵심적인 요소라고 할 수 있습니다.<br><br>

### 특징
---
* 게임 오브젝트와의 연결: 게임 오브젝트에 직접 연결되어 해당 오브젝트의 행동을 제어합니다.
* 라이프 사이클 메서드: Start, Update, FixedUpdate 등의 메서드를 통해 게임 오브젝트의 생명주기를 관리할 수 있습니다.
* 컴포넌트 기반 시스템: 다른 스크립트와 함께 게임 오브젝트에 추가되어 다양한 기능을 구현할 수 있습니다.
* 유니티 에디터 연동: Inspector 창을 통해 스크립트의 변수를 직관적으로 편집할 수 있습니다.
* 상속 가능: MonoBehaviour를 상속하여 자신만의 클래스를 만들 수 있습니다.
<br><br>

### 주요 Method
---
* Start(): 게임 오브젝트가 활성화될 때 한 번 호출됩니다. 초기화 작업에 주로 사용됩니다.
* Update(): 매 프레임마다 호출됩니다. 게임 로직을 구현하는 주된 메서드입니다.
* FixedUpdate(): 물리 시뮬레이션과 함께 고정된 간격으로 호출됩니다. 물리 연산이나 정밀한 타이밍이 필요한 작업에 사용됩니다.
* OnEnable(): 스크립트가 활성화될 때 호출됩니다.
* OnDisable(): 스크립트가 비활성화될 때 호출됩니다.
* OnDestroy(): 게임 오브젝트가 파괴될 때 호출됩니다.
<br><br>

## 사용법
---

1. 새 스크립트 생성: 유니티 에디터에서 새로운 C# 스크립트를 생성합니다.
2. MonoBehaviour 상속: 생성된 스크립트에서 MonoBehaviour를 상속받습니다.
3. 메서드 오버라이딩: 필요한 메서드(Start, Update 등)를 오버라이딩하여 게임 로직을 구현합니다.
4. 게임 오브젝트에 추가: 생성된 스크립트를 게임 오브젝트에 추가합니다.

<br><br>

```c#
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 10f;

    void Update()
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(horizontalInput, 0, verticalInput);
        transform.Translate(movement * speed * Time.deltaTime);
    }
}
```

## 주의점
---
* Update 메서드 오버헤드: Update 메서드는 매 프레임마다 호출되므로 너무 많은 연산을 하면 성능 저하가 발생할 수 있습니다. 불필요한 연산은 줄이고, 필요한 경우 FixedUpdate를 사용하는 것이 좋습니다.
* 메모리 관리: 더 이상 사용하지 않는 객체는 제거하여 메모리 누수를 방지해야 합니다.
* 코루틴: 복잡한 비동기 작업을 처리하기 위해 코루틴을 사용할 수 있지만, 잘못 사용하면 성능 문제가 발생할 수 있습니다.
<br><br>

<br>
[Top](#){: .btn .btn--primary }{: .align-right}