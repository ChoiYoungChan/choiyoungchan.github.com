---
title:  "[Unity] 유니티에서 스크립터블오브젝트(ScriptableObject) 개념 및 사용하는 방법 정리"
excerpt: Unity ScriptableObject

categories:
  - Unity
tags:
  - [Unity, ScriptableObject, 스크립터블오브젝트, 유니티]

toc: true
toc_sticky: true
 
date: 2023-10-15
last_modified_at: 2023-10-15
---

## 스크립터블오브젝트(ScriptableObject) 개념
---
ScriptableObject는 유니티에서 제공하는 컨테이너로 게임에서 사용되는 데이터를 저장하고 재사용하기 위한 강력한 도구입니다. <br>
게임 오브젝트에 직접 연결되지 않고, 에셋으로서 프로젝트 내에서 관리되며, Inspector 창에서 직관적으로 편집할 수 있습니다.
(간단하게, 스크립팅이 가능한 리소스 Object라고 생각하시면 됩니다.)

[유니티 공식 홈페이지](https://docs.unity3d.com/kr/2022.3/Manual/class-ScriptableObject.html)<br><br>

### 특징
* 데이터 저장: 게임 설정, 레벨 디자인, 아이템 정보 등 다양한 종류의 데이터를 저장할 수 있습니다.
* 재사용성: 여러 스크립트에서 동일한 데이터를 공유할 수 있어 코드의 재사용성을 높입니다.
* 에셋: 프로젝트 외부에서도 편집 가능하며, 버전 관리 시스템과의 연동이 용이합니다.
* 인스펙터 편집: Inspector 창에서 직관적인 UI를 통해 데이터를 편집할 수 있습니다.
<br><br>

### 장단점
---
#### 장점
* 데이터 관리: 게임 데이터를 중앙 집중화하여 관리하기 쉽습니다.
* 재사용성: 여러 스크립트에서 동일한 데이터를 공유할 수 있습니다.
* 확장성: 필요에 따라 새로운 ScriptableObject를 생성하여 기능을 확장할 수 있습니다.
* 편의성: Inspector 창을 통해 직관적으로 데이터를 편집할 수 있습니다.

#### 단점
* 성능: 많은 수의 ScriptableObject를 사용할 경우 메모리 사용량이 증가할 수 있습니다.
* 복잡성: 복잡한 데이터 구조를 표현하기 위해서는 추가적인 노력이 필요할 수 있습니다.
<br><br>

### 스크립터블오브젝트(ScriptableObject)와 PlayerPrefab의 차이점
---
<br>

![Image](https://github.com/user-attachments/assets/b40c4856-6a7c-45ed-b9c9-33f3183ea0ad)
<br><br>


### 스크립터블오브젝트(ScriptableObject)와 PlayerPrefab의 활용 예시
---
* 스크립터블 오브젝트
  * 캐릭터 능력치 데이터를 스크립터블 오브젝트로 저장하여 여러 캐릭터가 공유하도록 설정
  * 아이템 정보를 스크립터블 오브젝트로 저장하여 아이템 목록을 관리하고 게임에 적용
  * 레벨 디자인 데이터를 스크립터블 오브젝트로 저장하여 레벨을 구성하고 게임에 적용

* Player Prefab:
  * 플레이어 캐릭터를 Player Prefab으로 저장하여 게임 시작 시마다 플레이어 캐릭터 생성
  * 적 캐릭터를 Player Prefab으로 저장하여 다양한 적 캐릭터를 쉽게 생성하고 배치
  * 게임 오브젝트를 Player Prefab으로 저장하여 게임 월드를 구성하고 관리
<br><br>

## 생성 방법
---
1. ScriptableObject 상속
   * 새로운 C# 스크립트를 생성하고, ScriptableObject 클래스를 상속합니다.
   * CreateAssetMenu 속성을 사용하여 Asset 메뉴에서 생성할 수 있도록 설정합니다.

2. 변수 선언
   * 저장하고 싶은 데이터 타입의 변수를 선언합니다.
   * SerializeField 속성을 사용하여 Inspector 창에서 편집 가능하도록 설정합니다.

3. Inspector 설정
   * CustomEditor를 사용하여 Inspector 창의 UI를 커스터마이징할 수 있습니다.

<br>

먼저 아래와 같이 ScriptableObject로 만들 스크립트를 작성합니다.<br><br>

![scriptableobject_000](https://github.com/user-attachments/assets/1a4496ea-47d5-4a86-914e-7e44dac8d17c)<br><br>

그 다음은 아래와 같이 생성한 스크립트에서 오른쪽 클릭->메뉴에서 Create-> ScriptableObject를 선택하시면 됩니다.<br>

![scriptableobject_001](https://github.com/user-attachments/assets/7a243338-3bf2-41df-91ef-ee498c7e88ec)<br><br>

그러면 아래와 같이 ScriptableObject가 생성됩니다.<br>

![scriptableobject_002](https://github.com/user-attachments/assets/24e94f20-f1ed-4ba3-9a3d-0b0d0e5dae04) <br><br>


<br><br>

[사용 예시]
```c#
using UnityEngine;

[CreateAssetMenu(fileName = "New Item", menuName = "ScriptableObjects/Item")]
public class Item : ScriptableObject
{
    public string itemName;
    public Sprite itemIcon;
    public int itemValue;
}
```

[ScriptableObject을 사용하는 예시]
```c#
public class Player : MonoBehaviour
{
    public Item equippedItem;

    void Start()
    {
        // equippedItem에 저장된 아이템 정보 사용
        Debug.Log("Equipped item name: " + equippedItem.itemName);
    }
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}