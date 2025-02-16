---
title:  "[UE4] UPROPERTY & UFUNCTION Setting"
excerpt: UE4 UPROPERTY 및 UFUNCTION 설정

categories:
  - UE4
tags:
  - [NavMesh, UPROPERTY, UFUNCTION, UE4, 언리얼]

toc: true
toc_sticky: true
 
date: 2023-10-23
last_modified_at: 2023-10-23
---

## UPROPERTY와 UFUNCTION 개요
---
언리얼 엔진 4(UE4)에서 C++ 클래스를 블루프린트에서 사용할 수 있도록 연결하는 데 핵심적인 역할을 하는 두 가지 매크로가 바로 UPROPERTY와 UFUNCTION입니다.

* UPROPERTY: C++ 클래스의 변수를 블루프린트 노드에 노출시켜, 블루프린트에서 직접 값을 읽거나 수정할 수 있도록 합니다.
* UFUNCTION: C++ 클래스의 함수를 블루프린트 노드로 만들어, 블루프린트에서 직접 함수를 호출할 수 있도록 합니다.
<br><br>

## UPROPERTY 설정 목록 및 설명
---
UPROPERTY는 다양한 설정을 통해 변수의 노출 범위, 편집 가능 여부 등을 세밀하게 조절할 수 있습니다.

* EditAnywhere: 블루프린트 에디터에서 언제든지 값을 변경할 수 있도록 합니다.
* BlueprintReadOnly: 블루프린트에서 값을 읽기만 가능하고, 수정할 수 없습니다.
* EditDefaultsOnly: 디폴트 값만 편집 가능하며, 인스턴스 생성 후에는 값을 변경할 수 없습니다.
* Category: 변수를 그룹화하여 블루프린트 프로퍼티 창에서 보기 편하게 정리합니다.
* meta=(DisplayName="Custom Name"): 변수의 표시 이름을 커스텀으로 설정합니다.
* Replicated: 네트워크를 통해 다른 클라이언트와 값을 동기화합니다.
* Transient: 게임이 저장될 때 저장되지 않습니다.
* VisibleAnywhere: 블루프린트에서 어디서든 접근 가능합니다.
* BlueprintCallable: 블루프린트에서 함수를 호출할 수 있도록 합니다 (UFUNCTION과 중복되는 기능).

<br>

### 예시
---
```C++
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Player", meta=(DisplayName = "Player Name"))
FString PlayerName;
```
<br><br>

## UFUNCTION 설정 목록 및 설명
---
UFUNCTION은 UPROPERTY와 유사하게 다양한 설정을 통해 함수의 노출 범위, 호출 가능 여부 등을 조절할 수 있습니다.

* BlueprintCallable: 블루프린트에서 함수를 호출할 수 있도록 합니다.
* BlueprintPure: 함수가 순수 함수이며, 사이드 이펙트가 없음을 나타냅니다.
* Server, Client: 함수가 서버 또는 클라이언트에서 호출될 수 있도록 합니다.
* Reliable, Unreliable: 함수 호출의 신뢰성을 설정합니다.
* WithValidation: 함수 호출 시 유효성 검사를 수행합니다.
* Category, meta: UPROPERTY와 동일한 기능을 제공합니다.

<br>

### 예시
---
```C++
UFUNCTION(BlueprintCallable, Category = "Game")
void StartGame();
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}