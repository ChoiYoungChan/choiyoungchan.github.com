---
title:  "[Unity] NullReferenceException이 발생하는 주요 원인 및 해결 방법"
excerpt: Responding to NullReferenceException error

categories:
  - unity-error-respond
tags:
  - [Unity, 유니티, NullReferenceException, 널 익셉션]

toc: true
toc_sticky: true
 
date: 2024-02-17
last_modified_at: 2024-02-17
---

## NullReferenceException 개요
---
유니티 개발 중 자주 마주치는 NullReferenceException은 변수가 null 상태일 때 값에 접근하려고 할 때 발생하는 예외입니다.
이는 코드의 논리적 오류나, 객체 생성 시점의 문제, 또는 참조 해제 등 다양한 원인으로 발생할 수 있습니다.

<br>

## NullReferenceException이 발생하는 주요 원인
---

* 객체 초기화 누락 <br>
가장 흔한 원인 중 하나는 객체를 생성하지 않고 바로 사용하려고 할 때 발생합니다.
<br>

  [예시]
  ```C#
  MyClass myObject; // 객체 선언만 하고 초기화하지 않음

  myObject.MyMethod(); // NullReferenceException 발생!
  ```

  [해결]
  ```C#
  MyClass myObject = new MyClass(); // 객체 생성 및 초기화

  myObject.MyMethod(); // 정상 작동
  ```

* null 반환 값 처리 부재 <br>
메서드가 null을 반환할 수 있는 경우, 반환 값을 제대로 확인하지 않고 사용하면 예외가 발생할 수 있습니다.

  [예시]
  ```C#
  string FindName(int id)
  {
      // ... 특정 조건에서 null 반환 가능 ...
      return null; 
  }

  string name = FindName(123);
  int nameLength = name.Length; // name이 null이면 NullReferenceException 발생!
  ```

  [해결]
  ```C#
  string name = FindName(123);
  if (name != null)
  {
      int nameLength = name.Length; // 안전하게 사용
  }
  ```
<br>

* 이벤트 구독 해제 누락 <br>
이벤트를 구독한 객체가 해제되었지만 이벤트 구독이 해제되지 않은 경우, 이벤트가 발생할 때 null 객체에 접근하려고 시도하여 예외가 발생할 수 있습니다.

  * 설명: 이 경우는 좀 더 복잡한 시나리오에서 발생하며, 객체의 생명주기를 제대로 관리하지 못했을 때 발생합니다.
  * 해결: 객체가 더 이상 필요하지 않을 때 이벤트 구독을 해제해야 합니다.
<br><br> 

* Unity에서 Access할 객체를 찾지 못한 경우
  Find를 포함하여 다른 Object에 Access할 때 해당 Object를 찾지 못하는 경우에 NullReferenceException이 발생 할 수 있습니다.<br> 

  [예시]
  ```C#
  string FindName(int id)
  {
      // ... 특정 조건에서 null 반환 가능 ...
      return null; 
  }

  string name = FindName(123);
  int nameLength = name.Length; // name이 null이면 NullReferenceException 발생!
  ```

  [해결]
  ```C#
  string name = FindName(123);
  if (name != null)
  {
      int nameLength = name.Length; // 안전하게 사용
  }
  ```

 * 리플렉션 사용 시 잘못된 멤버 접근 <br>
  리플렉션을 사용하여 객체의 멤버에 동적으로 접근할 때, 존재하지 않는 멤버에 접근하려고 하면 예외가 발생할 수 있습니다.
    * 설명: 리플렉션은 런타임에 타입 정보를 분석하고 조작하는 기능으로, 잘못 사용하면 예외를 발생시킬 수 있습니다.
    * 해결: 리플렉션을 사용할 때는 멤버의 존재 여부를 확인하는 등 주의를 기울여야 합니다.

<br>

## 자주 발생하는 NullReferenceException 상황
---
* 씬 전환 시: 씬이 전환될 때 이전 씬의 오브젝트를 참조하려고 할 때
* 동적 생성된 오브젝트: Instantiate() 함수로 생성된 오브젝트가 제대로 초기화되지 않았을 때
* 싱글톤 패턴: 싱글톤 객체를 생성하거나 참조할 때
* 콜백 함수: 다른 스크립트에서 호출되는 콜백 함수 내에서

<br>

## NullReferenceException 예방 및 해결 방법
---
의외로 간단한 방법이지만 누구나 간과하는 부분입니다.

* 코드 리뷰: 다른 개발자와 코드를 검토하여 오류를 찾아냅니다.
* null 체크: 변수를 사용하기 전에 항상 null인지 확인합니다.
* 디버거 활용: 디버거를 사용하여 코드를 단계별로 실행하며 문제 발생 지점을 찾습니다.
* 단위 테스트: 코드의 각 부분을 테스트하여 오류를 조기에 발견합니다.

<br>

[Top](#){: .btn .btn--primary }{: .align-right}