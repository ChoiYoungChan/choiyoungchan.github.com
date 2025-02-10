---
title: "[Unity] 유니티의 생명주기에 관하여"
excerpt: Collision and Collider in Unity

categories:
  - Unity
tags:
  - [Unity, life time, 생명주기, 유니티]

toc: true
toc_sticky: true
 
date: 2024-06-20
last_modified_at: 2024-06-20
---

## 유니티 생명주기의 개요
---
Unity의 스크립트는 ```MonoBehaviour```클래스를 상속받아 만들어집니다. ```MonoBehaviour``` 클래스를 상속받은 스크립트가 포함된 게임 오브젝트는 Unity 엔진에 의해 일정한 흐름에 따라 자동으로 함수들이 호출되는데, 이러한 흐름을 생명주기라고 부릅니다.
<br>

## 주요 생명주기 함수
---
Unity에서 제공하는 주요 생명주기 함수들은 다음과 같습니다.
* Awake(): 스크립트가 활성화되든 비활성화되든 오브젝트가 생성될 때 단 한 번 호출됩니다. 주로 변수 초기화 등에 사용됩니다.
* OnEnable(): 오브젝트 또는 스크립트가 활성화될 때마다 호출됩니다.
* Start(): 스크립트가 활성화될 때 단 한 번 호출됩니다. ```Awake()``` 함수 이후에 호출되며, 주로 게임 로직 초기화 등에 사용됩니다.
* FixedUpdate(): 물리 연산과 관련된 업데이트를 처리하는 함수입니다. 일정한 간격으로 호출됩니다.
* Update(): 매 프레임마다 호출되는 함수입니다. 게임 로직, 사용자 입력 처리 등에 사용됩니다.
* LateUpdate(): Update() 함수가 호출된 후 호출되는 함수입니다. 카메라 이동 등과 같이 다른 오브젝트의 업데이트가 완료된 후 처리해야 하는 작업에 사용됩니다.
* OnTriggerEnter() / OnTriggerStay() / OnTriggerExit(): 트리거 콜라이더와 관련된 충돌 이벤트를 처리하는 함수입니다.
* OnCollisionEnter() / OnCollisionStay() / OnCollisionExit(): 일반 콜라이더와 관련된 충돌 이벤트를 처리하는 함수입니다.
* OnDisable(): 오브젝트 또는 스크립트가 비활성화될 때마다 호출됩니다.
* OnDestroy(): 오브젝트가 파괴될 때 단 한 번 호출됩니다.
<br><br>

## 생명주기 함수 호출 순서
---
Unity의 생명주기 함수들은 다음과 같은 순서로 호출됩니다.
* Awake()
* OnEnable()
* Start()
* FixedUpdate() (물리 연산 업데이트)
* Update() (게임 로직 업데이트)
* LateUpdate() (후처리 업데이트)
5~6번 반복
* OnTriggerEnter() / OnCollisionEnter() (충돌 시작 시)
* OnTriggerStay() / OnCollisionStay() (충돌 지속 시)
* OnTriggerExit() / OnCollisionExit() (충돌 종료 시)
* OnDisable() (오브젝트 비활성화 시)
* OnDestroy() (오브젝트 파괴 시)
<br><br>

## 생명주기 함수의 활용
---
각 생명주기 함수는 고유한 목적을 가지고 있습니다. 따라서 게임 개발 시 적절한 함수를 선택하여 사용하는 것이 중요합니다.
* Awake(): 변수 초기화, 컴포넌트 캐싱 등에 사용
* Start(): 게임 로직 초기화, 데이터 로딩 등에 사용
* FixedUpdate(): 물리 연산, 캐릭터 이동 등에 사용
* Update(): 사용자 입력 처리, 게임 로직 업데이트 등에 사용
* LateUpdate(): 카메라 이동, 그림자 처리 등에 사용
* OnTriggerEnter() / OnCollisionEnter(): 충돌 감지, 아이템 획득 등에 사용
* OnTriggerStay() / OnCollisionStay(): 충돌 지속 시 특정 동작 수행 등에 사용
* OnTriggerExit() / OnCollisionExit(): 충돌 종료 시 특정 동작 수행 등에 사용
* OnDisable(): 이벤트 연결 해제, 리소스 반환 등에 사용
* OnDestroy(): 오브젝트 파괴 시 처리해야 할 작업에 사용
<br><br>

## 유니티 공식 사이트의 생명주기
---
[유니티 공식 사이트](https://docs.unity3d.com/kr/2019.4/Manual/ExecutionOrder.html)
<br><br>

![Image](https://github.com/user-attachments/assets/6980bf03-7ba5-4e70-b27b-e29468ffe4cf)
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}