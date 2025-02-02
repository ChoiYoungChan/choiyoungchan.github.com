---
title:  "[Unity] 유니티에서 SerializeField의 기본 개념과 사용법"
excerpt: SerializeField in Unity

categories:
  - Unity Code
tags:
  - [SerializeField, 시리얼라이즈필드, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-02-15
last_modified_at: 2023-02-15
---

## 개요
---
```SerializeField```는 Unity에서 비공개(private) 필드를 인스펙터(Inspector)에 노출하고 싶을 때 사용하는 속성(Attribute)입니다. <br>
Unity의 직렬화 시스템을 통해 필드 값을 유지(persist) 하고, 에디터에서 편집 가능하도록 설정합니다.<br><br>


### 장단점
---
#### 장점
* 캡슐화 유지: private 접근 제어자를 유지하면서도 인스펙터에 노출할 수 있어, 데이터의 무분별한 접근을 막습니다.
* Unity 친화적: Unity의 직렬화 시스템을 통해 장면 저장, Prefab 저장, 빌드 시 데이터 유지가 가능합니다.
* 직관적 편집: 인스펙터를 통해 값을 쉽게 설정하거나 수정할 수 있어, 프로그래머가 아닌 사용자도 데이터를 조작할 수 있습니다.

#### 단점
* 런타임 전용 데이터 관리: 인스펙터에서 보이지만, 실제로 런타임에서만 필요한 데이터는 불필요하게 노출될 수 있습니다.
* 오용 가능성: SerializeField를 너무 남용하면 인스펙터가 복잡해지고, 캡슐화의 목적이 퇴색될 수 있습니다.


<br><br>


### 주의 사항
---
* Unity 직렬화 시스템의 한계
  * Unity는 클래스 중 **System.Serializable**로 선언된 클래스만 직렬화합니다.
  * Dictionary, HashSet과 같은 컬렉션 타입은 기본적으로 Unity에서 직렬화되지 않습니다.
  * private static 또는 const 필드는 직렬화되지 않습니다.

* 필드 타입
  * Unity는 직렬화 가능한 타입만 지원합니다.
    (ex. int, float, string, Vector3, GameObject, 사용자 정의 클래스 등)

* 복잡한 데이터 구조
  * Unity는 중첩된 클래스 구조 또는 참조형 데이터에서 순환 참조(Circular Reference)를 제대로 직렬화하지 못할 수 있습니다.

<br><br>

## 사용 예시
---

[사용 예시]

```c#
using UnityEngine;
using System;

[Serializable] // 사용자 정의 클래스도 직렬화 가능하도록 설정
public class Weapon
{
    public string name;
    public int damage;
    public float range;
}

public class SerializeFieldExample : MonoBehaviour
{
    // 1. SerializeField를 사용한 private 필드
    [SerializeField] private int playerHealth = 100;
    [SerializeField] private float speed = 5.0f;
    [SerializeField] private string playerName = "Hero";

    // 2. 직렬화 가능한 사용자 정의 클래스
    [SerializeField] private Weapon equippedWeapon;

    // 3. 배열 직렬화
    [SerializeField] private Weapon[] weaponInventory;

    // 4. List 직렬화
    [SerializeField] private System.Collections.Generic.List<Weapon> weaponList;

    // 5. 직렬화 불가능한 Dictionary 예제
    private System.Collections.Generic.Dictionary<string, int> weaponMap; // 직렬화되지 않음

    private void Start()
    {
        // 직렬화된 데이터를 사용
        Debug.Log($"Player: {playerName}, Health: {playerHealth}");
        Debug.Log($"Equipped Weapon: {equippedWeapon.name} (Damage: {equippedWeapon.damage})");
        
        // 런타임에서 weaponMap 초기화
        weaponMap = new System.Collections.Generic.Dictionary<string, int>
        {
            { "Sword", 10 },
            { "Bow", 7 }
        };

        Debug.Log("Weapon Map Initialized at Runtime.");
    }
}

```

## SerializeField를 사용할 때의 팁
---
* 유효성 검사: 값이 잘못 설정되지 않도록 제한을 추가하세요. 예를 들어, Range 속성으로 값 범위를 제한할 수 있습니다:

```c#
[SerializeField, Range(0, 100)]
private int playerHealth;
```

* 구조화된 데이터 관리: 사용자 정의 클래스를 사용하면 복잡한 데이터를 그룹화하고 직렬화하기 쉽습니다.
* 적절한 노출: 정말 필요한 필드만 인스펙터에 노출하고, 지나치게 많은 SerializeField를 피하는게 좋습니다.

<br>

[Top](#){: .btn .btn--primary }{: .align-right}