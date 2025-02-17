---
title:  "[UE4] 언리얼엔진에서 BindAction의 개념과 사용법"
excerpt: BindAction in Unreal Engine 4

categories:
  - UE4
tags:
  - [바인드, BindAction, UE4, 언리얼]

toc: true
toc_sticky: true
 
date: 2023-10-23
last_modified_at: 2023-10-23
---

## BindAction 개요
---
BindAction은 게임에서 "특정 행동"과 "입력"을 연결해 주는 도구입니다. 마치 스위치와 전구의 관계와 같아요. 스위치를 누르면 (입력), 전구에 불이 들어오는 (행동) 것처럼, 특정 키를 누르거나 마우스 버튼을 클릭하면 (입력), 게임 속 캐릭터가 점프하거나 공격하는 등의 특정 행동 (행동)을 실행하도록 연결해 주는 것이 바로 BindAction입니다.<br>

예를 들어, "스페이스 바"를 누르면 "점프"하는 행동을 하도록 설정할 수 있습니다. 이때 "스페이스 바"는 입력, "점프"는 행동이 되는 것이죠. BindAction은 이 둘을 연결해 주는 역할을 합니다.
<br><br>

## 사용법
---
BindAction을 사용하는 방법은 마치 레고 블록을 조립하는 것과 같이 간단합니다. 필요한 블록들을 가져와서 정해진 규칙에 따라 연결하면 멋진 작품이 만들어지는 것처럼, BindAction도 정해진 단계를 따라 사용하면 됩니다.

* 입력 매핑 설정: 먼저 프로젝트 설정에서 어떤 입력을 사용할지 정해야 합니다. "스페이스 바", "마우스 왼쪽 버튼", "A 키" 등 사용할 입력을 프로젝트 설정의 "입력" 메뉴에서 추가합니다. 이때 각 입력에 이름을 붙여줍니다. 예를 들어 "Jump"라는 이름으로 "스페이스 바"를 매핑할 수 있습니다.
* BindAction 함수 사용: C++ 코드에서 BindAction 함수를 사용하여 입력과 행동을 연결합니다. SetupPlayerInputComponent 함수 안에서 다음과 같은 형태로 사용합니다.
```C++
// "Jump"라는 이름의 입력에 "OnJump" 함수를 연결
InputComponent->BindAction("Jump", IE_Pressed, this, &ACharacter::OnJump);
```
[코드 설명]
```
"Jump": 프로젝트 설정에서 정의한 입력 이름
IE_Pressed: 입력을 "눌렀을 때" 행동을 실행
this: 현재 액터
&ACharacter::OnJump: 실행할 함수
```
<br>

* 행동 함수 구현: 실제로 어떤 행동을 할지 함수를 만들어야 합니다. 위의 예시에서는 OnJump 함수를 만들어 점프 로직을 구현해야 합니다.

```C++
void ACharacter::OnJump()
{
    // 점프 로직 구현
    Jump();
}
```
<br><br>

[간단한 예시]
```C++
// 헤더 파일 (Character.h)
UCLASS()
class MYPROJECT_API ACharacter : public ACharacter
{
    GENERATED_BODY()

public:
    // ...

protected:
    // ...

    void OnJump(); // 점프 함수 선언

    // ...
};

// 소스 파일 (Character.cpp)
void ACharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &ACharacter::OnJump);
}

void ACharacter::OnJump()
{
    Jump();
}
```
<br><br>

[응용 버전] : 점프 버튼을 길게 누르면 더 높이 점프하는 예시 코드입니다.

```c++
// 헤더 파일 (Character.h)
// ...

protected:
    // ...

    void OnJumpPressed(); // 점프 버튼을 눌렀을 때 호출되는 함수
    void OnJumpReleased(); // 점프 버튼을 뗐을 때 호출되는 함수

    bool bIsJumping; // 점프 중인지 여부를 저장하는 변수

    // ...

// 소스 파일 (Character.cpp)
void ACharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &ACharacter::OnJumpPressed);
    PlayerInputComponent->BindAction("Jump", IE_Released, this, &ACharacter::OnJumpReleased);
}

void ACharacter::OnJumpPressed()
{
    bIsJumping = true;
    Jump(); // 기본 점프
}

void ACharacter::OnJumpReleased()
{
    bIsJumping = false;
}

void ACharacter::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);

    if (bIsJumping)
    {
        // 점프 버튼을 누르고 있는 동안 추가적인 힘을 가함
        ACharacter::LaunchCharacter(FVector(0, 0, 100), false, false);
    }
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}