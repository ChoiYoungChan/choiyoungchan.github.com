---
title:  "[Unity] 유니티에서 NonSerialized의 기본 개념과 사용법"
excerpt: NonSerialized in Unity

categories:
  - Unity Code
tags:
  - [NonSerialized, 논시리얼라이즈필드, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-02-20
last_modified_at: 2023-02-20
---

## 개요
---
```NonSerialized```는 Unity에서 특정 필드를 직렬화하지 않도록 명시적으로 지정하는 속성(Attribute)입니다. <br>
Unity의 직렬화 시스템은 기본적으로 public 필드와 [SerializeField]가 적용된 private 필드를 직렬화합니다. 그러나 [NonSerialized]를 사용하면 Unity가 해당 필드를 직렬화에서 제외합니다. <br><br>

### 목적과 특징
---
* 직렬화 제외
  * Unity가 직렬화할 필요 없는 데이터를 명시적으로 제외합니다.<br>
    예를 들어, 런타임에만 사용되는 캐시 데이터나 참조값 등은 직렬화가 필요하지 않습니다.

* 데이터 보호
  * 인스펙터에 표시되지 않도록 하고, Unity 장면 또는 Prefab에 데이터를 저장하지 않습니다.

* 사용 범위
  * 직렬화 가능 필드에만 적용됩니다.
  * private 필드에는 필요하지 않습니다. Unity는 기본적으로 private 필드를 직렬화하지 않습니다
    (단, [SerializeField]가 없는 경우).

* 런타임 전용 데이터 관리
  * 런타임 동안에만 필요한 값을 저장하거나 초기화해야 하는 경우 유용합니다.
<br><br>

### 장단점
---
#### 장점
* 불필요한 직렬화 방지: 런타임 전용 데이터가 직렬화되지 않도록 하여 성능을 최적화합니다.
* 데이터 노출 방지: 의도적으로 데이터를 인스펙터에 노출하지 않음으로써 코드의 가독성을 유지하고 오류 가능성을 줄입니다.
* 직렬화 오류 방지: Unity 직렬화 시스템이 처리할 수 없는 타입에 사용하면 경고 또는 오류를 피할 수 있습니다.

#### 단점
* 값 초기화 불가: 직렬화되지 않으므로, Unity가 장면이나 Prefab을 저장/로드할 때 값을 유지하지 않습니다.
* 유지보수 어려움: 잘못된 사용은 나중에 직렬화가 필요할 때 혼란을 초래할 수 있습니다.

<br><br>


### 주의 사항
---
1. Unity 직렬화의 범위
   * Unity는 다음 필드만 기본적으로 직렬화합니다:
     * public 필드
     * [SerializeField]가 적용된 private 필드 

2. 필드 타입 제한
   * Unity 직렬화 시스템은 특정 데이터 타입(예: int, float, GameObject, 사용자 정의 클래스 등)만 직렬화할 수 있습니다.
   * 직렬화 불가능한 데이터 타입(예: Dictionary, HashSet)은 Unity에서 무시되며, [NonSerialized]를 추가하지 않아도 기본적으로 직렬화되지 않습니다.

3. 런타임 데이터
   * 런타임에서 계산되거나 생성되는 임시 데이터는 직렬화하지 않아야 합니다.

<br><br>

## 사용 예시
---

[사용 예시]

```c#
using UnityEngine;
using System;

[Serializable] // 사용자 정의 클래스 직렬화 가능
public class PlayerStats
{
    public int health;
    public int mana;
}

public class NonSerializedExample : MonoBehaviour
{
    // 1. 인스펙터에 표시되는 직렬화 필드
    [SerializeField] private PlayerStats stats;

    // 2. NonSerialized 필드 (직렬화 제외)
    [NonSerialized] public int runtimeOnlyData; // 런타임 전용 데이터

    // 3. 직렬화되지 않는 C# 타입
    private System.Collections.Generic.Dictionary<string, int> cachedValues;

    // 4. NonSerialized는 private 필드에 필요하지 않음
    private int privateData; // 자동으로 직렬화되지 않음

    private void Start()
    {
        // 런타임 전용 데이터 초기화
        runtimeOnlyData = 42;
        Debug.Log($"Runtime-Only Data: {runtimeOnlyData}");

        // 런타임에 Dictionary 초기화
        cachedValues = new System.Collections.Generic.Dictionary<string, int>
        {
            { "HealthPotion", 3 },
            { "ManaPotion", 5 }
        };
    }

    private void Update()
    {
        // Dictionary를 활용해 데이터 조회
        if (cachedValues.TryGetValue("HealthPotion", out int value))
        {
            Debug.Log($"Health Potion Count: {value}");
        }
    }
}
```

## NonSerialized와 SerializeField의 비교
---
<br>

![NonserializeField](https://github.com/user-attachments/assets/85ef6926-582d-4f1d-ac13-819c50971d81)

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}