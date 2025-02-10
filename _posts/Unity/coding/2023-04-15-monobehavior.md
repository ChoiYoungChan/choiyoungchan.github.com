---
title:  "[Unity] 유니티에서 Monobehavior의 기본 개념과 사용법"
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

## MonoBehaviour의 역할과 중요성
---
MonoBehaviour는 유니티 엔진과 스크립트 간의 소통을 가능하게 하는 다리 역할을 합니다. 게임 오브젝트에 부착된 스크립트는 MonoBehaviour를 상속받아 유니티 엔진이 제공하는 다양한 기능과 이벤트에 접근하고, 게임 오브젝트의 행동을 정의합니다.<br>
<br>
MonoBehaviour가 없다면 우리는 게임 오브젝트를 움직이거나, 충돌을 감지하거나, 사용자 입력을 처리하는 등의 작업을 수행할 수 없습니다. 즉, MonoBehaviour는 유니티 게임 개발의 기본이자 핵심입니다.
<br><br>

### 특징
---
* 게임 오브젝트와의 연결: MonoBehaviour 스크립트는 게임 오브젝트에 부착되어 해당 오브젝트의 행동을 직접 제어합니다. 마치 인형극에서 인형에 실을 연결하여 움직이는 것과 같습니다. 스크립트의 코드는 게임 오브젝트의 위치, 회전, 크기 등을 변경하고, 다른 컴포넌트들을 제어하며, 게임 로직을 수행합니다.

* 라이프 사이클 메서드: MonoBehaviour는 게임 오브젝트의 생명주기에 따라 자동으로 호출되는 다양한 라이프 사이클 메서드를 제공합니다. 이러한 메서드들을 통해 게임 오브젝트의 생성, 업데이트, 소멸 시점에 맞춰 필요한 작업을 수행할 수 있습니다.

  - Start(): 게임 오브젝트가 처음 생성되고 활성화될 때 단 한 번 호출됩니다. 주로 변수 초기화, 컴포넌트 참조, 초기 게임 설정 등에 사용됩니다.
  - Update(): 매 프레임마다 호출됩니다. 사용자 입력 처리, 게임 로직 업데이트, 애니메이션 제어 등 가장 빈번하게 사용되는 메서드입니다.
  - FixedUpdate(): 물리 시뮬레이션과 함께 고정된 시간 간격으로 호출됩니다. 물리 연산, 캐릭터 이동, 충돌 처리 등 물리 관련 작업에 사용됩니다.
  - LateUpdate(): Update() 함수가 호출된 후 호출됩니다. 카메라 이동, 그림자 처리 등 다른 오브젝트의 업데이트가 완료된 후 처리해야 하는 작업에 사용됩니다.
  - OnEnable(): 스크립트가 활성화될 때마다 호출됩니다.
  - OnDisable(): 스크립트가 비활성화될 때마다 호출됩니다.
  - OnDestroy(): 게임 오브젝트가 파괴될 때 단 한 번 호출됩니다.
<br><br>

* 컴포넌트 기반 시스템: 유니티는 컴포넌트 기반 시스템을 통해 게임 오브젝트에 다양한 기능을 추가할 수 있습니다. MonoBehaviour 스크립트 또한 컴포넌트의 일종이며, 다른 컴포넌트들과 함께 게임 오브젝트에 추가되어 시너지를 발휘합니다. 예를 들어, 충돌 처리를 위해 Collider 컴포넌트와 Rigidbody 컴포넌트를 함께 사용할 수 있습니다.

* 유니티 에디터 연동: MonoBehaviour 스크립트는 유니티 에디터의 Inspector 창과 연동되어 스크립트의 변수를 직관적으로 편집할 수 있습니다. 이를 통해 코드를 수정하지 않고도 게임의 설정을 변경하거나 테스트할 수 있습니다.

* 상속 가능: MonoBehaviour 클래스를 상속하여 자신만의 클래스를 만들 수 있습니다. 이를 통해 MonoBehaviour의 기능을 확장하거나 특정 목적에 맞는 기능을 추가할 수 있습니다.
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

1. 새 스크립트 생성: 유니티 에디터의 Project 창에서 마우스 오른쪽 버튼을 클릭하고, Create > C# Script를 선택하여 새로운 C# 스크립트를 생성합니다.
2. MonoBehaviour 상속: 생성된 스크립트 파일(.cs)을 열어 클래스 이름 뒤에``` : MonoBehaviour```를 추가하여 MonoBehaviour 클래스를 상속받습니다.
3. 메서드 오버라이딩: 필요한 메서드(Start, Update, FixedUpdate 등)를 오버라이딩하여 게임 로직을 구현합니다.
4. 게임 오브젝트에 추가: 생성된 스크립트 파일을 유니티 에디터의 Hierarchy 창에 있는 게임 오브젝트에 드래그 앤 드롭하여 스크립트를 게임 오브젝트에 추가합니다.
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
* Update 메서드 오버헤드: Update() 메서드는 매 프레임마다 호출되므로 너무 많은 연산을 하면 성능 저하가 발생할 수 있습니다. 불필요한 연산은 줄이고, 필요한 경우 FixedUpdate() 메서드를 사용하거나 코루틴을 활용하는 것이 좋습니다.
* 메모리 관리: 더 이상 사용하지 않는 객체는 ```Destroy()``` 메서드를 사용하여 제거하고, 리소스를 해제하여 메모리 누수를 방지해야 합니다.
* 코루틴: 복잡한 비동기 작업을 처리하기 위해 코루틴을 사용할 수 있지만, 잘못 사용하면 성능 문제가 발생할 수 있습니다. 코루틴을 사용할 때는 주의하여 코드를 작성해야 합니다.
<br><br>

## MonoBehaviour 활용 팁
---
* 컴포넌트 캐싱: GetComponent() 메서드를 자주 호출하면 성능 저하가 발생할 수 있습니다. Start() 메서드에서 컴포넌트를 한 번 가져와 변수에 저장해두고 사용하는 것이 좋습니다.
* SerializeField: SerializeField 키워드를 사용하면 private 변수를 Inspector 창에 노출시켜 편집할 수 있습니다.
* [Header]: [Header("My Header")]를 사용하면 Inspector 창에 그룹 제목을 추가하여 변수들을 정리할 수 있습니다.
* [Tooltip]: [Tooltip("This is a tooltip")]을 사용하면 변수에 대한 설명을 툴팁으로 표시할 수 있습니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}