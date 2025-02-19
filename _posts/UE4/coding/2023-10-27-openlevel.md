---
title:  "[UE4] 언리얼 엔진의 OpenLevel의 개념과 사용법"
excerpt: OpenLevel in Unreal Engine

categories:
  - UE4
tags:
  - [OpenLevel, UE4, 언리얼]

toc: true
toc_sticky: true
 
date: 2023-10-23
last_modified_at: 2023-10-23
---

## OpenLevel 개요
---
OpenLevel은 UE4에서 현재 레벨(맵)을 닫고 새로운 레벨을 로드하는 함수입니다. 게임의 스테이지 이동, 메뉴 화면 전환, 컷신 재생 후 게임으로 복귀 등 다양한 상황에서 사용됩니다. <br>마치 연극 무대에서 막이 바뀌는 것과 같습니다. 이전 막이 끝나고 막이 내려온 뒤 새로운 배경과 배우들이 등장하는 것처럼, OpenLevel은 현재 레벨을 내리고 새로운 레벨을 불러오는 역할을 합니다.
<br><br>

### 블루프린트에서의 사용
---
블루프린트에서는 "Open Level" 노드를 사용하여 ```OpenLevel``` 함수를 호출할 수 있습니다. 노드의 입력 핀은 C++ 함수의 인자와 동일한 역할을 합니다.

[블루프린트 이미지]
<br>

### 심리스 트래블 (Seamless Travel)
---
심리스 트래블은 레벨 전환 시 로딩 화면을 부드럽게 처리하여 사용자 경험을 향상시키는 기능입니다. ```OpenLevel``` 함수의 세 번째 인자를 ```true```로 설정하면 심리스 트래블이 활성화됩니다. 심리스 트래블을 사용하면 다음과 같은 효과를 얻을 수 있습니다.

* 로딩 화면이 부드럽게 페이드 인/아웃됩니다.
* 플레이어의 위치, 회전, 속도 등의 정보를 새로운 레벨로 전달할 수 있습니다.
* 네트워크 게임에서 클라이언트와 서버의 연결을 유지하면서 레벨을 전환할 수 있습니다.

<br>

### 레벨 스트리밍 (Level Streaming)과의 차이점
---
OpenLevel은 완전히 새로운 레벨을 로드하는 반면, 레벨 스트리밍은 현재 레벨에 추가적인 서브 레벨을 로드하거나 언로드하는 방식입니다. 마치 책의 새로운 장을 펼치는 것과 책갈피를 꽂아두었다가 다시 펼치는 것의 차이와 같습니다. OpenLevel은 완전히 새로운 게임 환경으로 전환할 때 사용하고, 레벨 스트리밍은 넓은 맵을 효율적으로 관리하거나 특정 영역만 로드/언로드하여 성능을 최적화할 때 사용합니다.

<br>

## 예시
---
```C++
#include "Kismet/GameplayStatics.h"

// ...

UGameplayStatics::OpenLevel(this, FName("NewLevelName"), true, FString("?Option1=Value1?Option2=Value2"));
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}