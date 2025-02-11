---
title:  "[Unity] 유니티 콜리전(Collision) 콜라이더(Collider) 차이 및 사용법"
excerpt: Collision and Collider in Unity

categories:
  - Unity
tags:
  - [Unity, Collision, Collider, 콜리전, 콜라이더, 유니티]

toc: true
toc_sticky: true
 
date: 2024-06-20
last_modified_at: 2024-06-20
---

## 콜리전(Collision) 콜라이더(Collider) 개념
---

콜리전(Collision)이란?
콜리전은 게임 오브젝트(Game Object)들이 서로 충돌하는 현상을 의미합니다. 예를 들어, 게임 속 캐릭터가 벽에 부딪히거나, 두 자동차가 충돌하는 상황 등이 콜리전에 해당합니다.<br>
이러한 충돌을 감지하고 처리하는 것은 게임의 현실감과 몰입도를 높이는 데 매우 중요한 역할을 하는데, Unity는 이러한 충돌을 감지하고, 충돌에 대한 다양한 처리를 수행할 수 있도록 기능을 제공합니다.
<br><br>

콜라이더(Collider)란?
콜라이더는 게임 오브젝트의 물리적인 형태를 정의하는 컴포넌트입니다. 눈에는 보이지 않지만, 게임 오브젝트가 다른 오브젝트와 충돌할 수 있는 영역을 나타냅니다. <br>
마치 물체의 겉모습을 감싸는 보이지 않는 껍질과 같습니다. 콜라이더가 없다면 게임 오브젝트는 서로를 통과하게 됩니다.
<br><br>

### 다양한 종류의 콜라이더
---
Unity는 다양한 형태의 콜라이더를 제공하며, 게임 오브젝트의 모양에 따라 적절한 콜라이더를 선택하여 사용할 수 있습니다.

* Box Collider: 직육면체 형태의 콜라이더입니다. 상자 모양의 오브젝트에 적합합니다.
* Sphere Collider: 구 형태의 콜라이더입니다. 공이나 구슬 모양의 오브젝트에 적합합니다.
* Capsule Collider: 캡슐 형태의 콜라이더입니다. 사람이나 원통형 오브젝트에 적합합니다.
* Mesh Collider: 오브젝트의 메시(mesh) 형태와 동일한 형태의 콜라이더입니다. 복잡한 모양의 오브젝트에 정확한 충돌 처리를 제공하지만, 계산 비용이 많이 들 수 있습니다.
* Circle Collider2D (2D 게임): 원 형태의 2D 콜라이더입니다.
* Box Collider2D (2D 게임): 사각형 형태의 2D 콜라이더입니다.
* Polygon Collider2D (2D 게임): 다각형 형태의 2D 콜라이더입니다. 복잡한 2D 모양에 적합합니다.
* Edge Collider2D (2D 게임): 선분 형태의 2D 콜라이더입니다.
<br><br>

### 트리거(Trigger)
---
콜라이더의 Is Trigger 속성을 활성화하면 콜라이더는 트리거로 동작합니다. 트리거는 충돌을 감지하지만, 물리적인 충돌 반응은 발생시키지 않습니다. 주로 특정 영역에 진입했을 때 이벤트를 발생시키는 용도로 사용됩니다. 예를 들어, 아이템 획득 영역, 문 진입 영역 등에 사용될 수 있습니다.

OnTriggerEnter, OnTriggerStay, OnTriggerExit 등의 콜백 함수를 사용하여 트리거 이벤트를 처리할 수 있습니다.
<br><br>

### 충돌 이벤트 함수
---
충돌 발생 시 호출되는 콜백 함수들을 사용하여 충돌에 대한 처리를 구현할 수 있습니다.

* OnCollisionEnter(Collision collision): 충돌이 시작될 때 한 번 호출됩니다.
* OnCollisionStay(Collision collision): 충돌이 지속되는 동안 매 프레임마다 호출됩니다.
* OnCollisionExit(Collision collision): 충돌이 끝날 때 한 번 호출됩니다.
<br><br>

### 충돌 매트릭스(Collision Matrix)
---
Unity 에디터의 ```Edit``` -> ```Project Settings``` -> ```Physics``` 또는 ```Physics2D```에서 충돌 매트릭스를 설정할 수 있습니다. 이를 통해 어떤 레이어(Layer)끼리 충돌을 감지할지 설정할 수 있습니다. 예를 들어, "Player" 레이어와 "Enemy" 레이어만 충돌하도록 설정하여 불필요한 충돌 계산을 줄일 수 있습니다.
<br><br>

### 충돌(Collision)과 콜라이더(Collider)의 관계
---
충돌은 콜라이더를 가진 게임 오브젝트 간에 발생합니다. 즉, 콜라이더는 충돌을 감지하는 역할을 하고, 충돌이 발생하면 Unity 엔진은 충돌 이벤트를 발생시킵니다. 이러한 충돌 이벤트를 통해 게임 로직을 구현할 수 있습니다.
<br><br>

### 리지드바디(Rigidbody) 컴포넌트와의 관계
---
콜리전은 리지드바디(Rigidbody)컴포넌트와 함께 사용되는 경우가 많습니다. 리지드바디는 게임 오브젝트에 물리적인 속성(질량, 중력 등)을 부여하여, 충돌 시 물리적인 반응을 시뮬레이션할 수 있도록 합니다. 즉, 콜라이더는 충돌 영역을 정의하고, 리지드바디는 충돌에 따른 움직임을 계산합니다.

* Rigidbody가 있는 오브젝트는 물리 엔진의 영향을 받아 중력, 충돌 등의 물리적인 효과를 받습니다.
* Rigidbody가 없는 오브젝트는 충돌은 감지하지만, 물리적인 반응을 보이지 않습니다.
<br><br>

### 각각의 장단점
---
#### 장점
콜리전(Collision)
* 직관적인 상호작용: 게임 오브젝트 간의 물리적인 충돌을 시뮬레이션하여 현실감 있는 상호작용을 구현할 수 있습니다.
* 다양한 이벤트 발생: 충돌 발생 시 다양한 이벤트를 발생시켜 게임 로직을 구현하는 데 활용할 수 있습니다. (OnCollisionEnter, OnCollisionStay, OnCollisionExit 등)
* 물리 엔진 활용: Unity의 물리 엔진을 활용하여 충돌에 따른 다양한 물리적 효과를 쉽게 구현할 수 있습니다. (마찰, 반발력 등)
<br><br>

콜라이더(Collider)
* 간편한 충돌 감지: 콜라이더를 통해 게임 오브젝트 간의 충돌 여부를 쉽게 감지할 수 있습니다.
* 다양한 형태 제공: 다양한 형태의 콜라이더를 제공하여 게임 오브젝트의 모양에 맞는 충돌 영역을 설정할 수 있습니다. (Box Collider, Sphere Collider, Capsule Collider, Mesh Collider 등)
* 트리거 기능 제공: Is Trigger 속성을 활성화하여 충돌은 감지하되 물리적인 반응은 발생시키지 않는 트리거 콜라이더를 사용할 수 있습니다.
<br><br>

#### 단점
콜리전(Collision)
* 성능 저하 가능성: 복잡한 충돌 계산은 게임 성능 저하를 유발할 수 있습니다. 특히 많은 오브젝트가 동시에 충돌하는 상황에서 성능 문제가 발생할 수 있습니다.
* 예측 불가능한 상황 발생 가능: 물리 엔진의 특성상 예측 불가능한 충돌 상황이 발생할 수 있습니다.
* 세밀한 제어 어려움: 충돌 자체는 단순히 부딪히는 현상만 감지하므로, 세밀한 상호작용을 구현하려면 추가적인 로직이 필요합니다.
<br><br>

콜라이더(Collider)
* 성능 문제: 복잡한 형태의 콜라이더(Mesh Collider 등)는 충돌 계산에 많은 비용이 소모되어 성능 저하를 유발할 수 있습니다.
* 정확도 문제: 단순한 형태의 콜라이더는 실제 오브젝트 모양과 차이가 있어 정확한 충돌 감지가 어려울 수 있습니다.
* 콜라이더 설정 필요: 각 게임 오브젝트에 적절한 콜라이더를 설정해야 하며, 충돌 상황에 따라 콜라이더 설정을 조절해야 할 수 있습니다.
<br><br>

## 예제
---

충돌 이벤트를 처리하는 간단한 예시 코드입니다.
```C#
using UnityEngine;

public class CollisionHandler : MonoBehaviour
{
    private void OnCollisionEnter(Collision collision)
    {
        // 충돌한 오브젝트의 이름 출력
        Debug.Log(gameObject.name + " collided with " + collision.gameObject.name);

        // 충돌한 오브젝트가 "Player" 태그를 가지고 있다면
        if (collision.gameObject.CompareTag("Player"))
        {
            // 특정 동작 수행 (예: 점수 증가)
            Debug.Log("Player collided!");
        }
    }

    private void OnTriggerEnter(Collider other) {
        if (other.CompareTag("Player"))
        {
            Debug.Log("Player entered the trigger!");
        }
    }
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}