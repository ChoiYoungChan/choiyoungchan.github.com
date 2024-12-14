---
title:  "[Git] git submodule에 관하여"
excerpt: git submodule에 관하여

categories:
  - Git
tags:
  - [Github, Git, git submodule, 깃, 서브모듈]

toc: true
toc_sticky: true
 
date: 2022-01-10
last_modified_at: 2022-01-10
---


## git submodule이란?
---
하나의 Git 프로젝트 안에 다른 Git 프로젝트를 하위 디렉토리로 포함시키는 기능입니다. 마치 레고 블록처럼, 독립적인 여러 프로젝트를 하나의 큰 프로젝트로 묶어 관리할 수 있게 해줍니다.
<br><br>

### 사용하는 이유
---
* 모듈화: 복잡한 프로젝트를 작은 단위의 모듈로 나누어 관리하여 코드 재사용성을 높이고 유지보수를 용이하게 합니다.
* 독립성: 각 submodule은 별도의 Git 저장소로 관리되므로, 각각의 프로젝트를 독립적으로 개발하고 배포할 수 있습니다.
* 버전 관리: submodule은 특정 커밋을 가리키므로, 프로젝트의 특정 버전에 맞는 submodule을 사용할 수 있습니다.
<br><br>

### 역할
---
* 외부 라이브러리 포함: 외부에서 개발된 라이브러리를 프로젝트에 포함시킬 때 사용합니다.
* 공통 코드 관리: 여러 프로젝트에서 공통적으로 사용되는 코드를 하나의 submodule로 만들어 관리합니다.
* 큰 프로젝트 분할: 너무 커진 프로젝트를 작은 단위로 분할하여 관리합니다.

<br><br>

### 주의해야될 점
---
* 복잡성: submodule은 프로젝트 관리를 더 복잡하게 만들 수 있습니다.
* 충돌: 다른 개발자와 협업할 때 submodule 관련 충돌이 발생할 수 있습니다.
* 클론 시 주의: submodule을 포함한 프로젝트를 clone 할 때는 ```--recursive``` 옵션을 사용해야 submodule도 함께 clone됩니다.
* detached HEAD 상태: submodule 내에서 작업할 때는 detached HEAD 상태가 될 수 있으므로 주의해야 합니다.
* submodule 업데이트 전 커밋: submodule을 업데이트하기 전에 반드시 변경 사항을 커밋해야 합니다.
* submodule 삭제: git submodule deinit 명령어로 submodule을 삭제할 수 있습니다. 하지만 실제 파일은 삭제되지 않으므로 수동으로 삭제해야 합니다.

<br><br>

## 사용 예시
---


[submodule 추가하기]
```
git submodule add <submodule 저장소 URL> <프로젝트 내 위치>
```

* <submodule 저장소 URL>: 추가할 submodule의 Git 저장소 주소
* <프로젝트 내 위치>: submodule을 추가할 프로젝트 내 디렉토리<br>


[submodule 업데이트]
```
git submodule update
```

* 모든 submodule을 최신 버전으로 업데이트합니다.
* 특정 submodule만 업데이트하려면: git submodule update <submodule 이름><br>


[submodule 초기화]
```
git submodule init
```

[submodule 상태 확인]
```
git submodule status
```


<br>
[Top](#){: .btn .btn--primary }{: .align-right}