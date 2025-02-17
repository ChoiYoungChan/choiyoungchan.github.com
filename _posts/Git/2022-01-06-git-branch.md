---
title:  "[GIT] 깃 허브 브랜치(Branch)에 대하여(예시 Git 명령어 포함)"
excerpt: Merge in GitHurb

categories:
  - Git
tags:
  - [Branch, Git, 깃, 브랜치]

toc: true
toc_sticky: true
 
date: 2022-01-05
last_modified_at: 2022-01-05
---


## 개요
---
Git에서 브랜치는 독립적인 Working Directory 를 의미합니다. 현재의 버전으로 다른 버전(기존 코드를 복사해와 완전히 새로운 독립 공간을 만듬)을 만들어서 가지를 치는것 입니다.<br>
일반적으로 여러가지 버전의 브랜치를 만들어 보고 이를 합치는 식으로 작업하는데, 
이렇게 분기를 만드는 브랜치 생성을 통해 동일한 소스코드를 기반으로 서로 다른 버전을 만들거나, 서로 다른 작업을 할 수 있다.
<br>

### 사용 용도 & 전략
---
* 다른 방식의 코드로 테스트해보기 위해 테스트 버전을 만들 branch를 만듭니다.
* 백업 해두기 위해 branch를 만든다.
* **협업시 각각의 Collaborator 마다 본인만의 branch를 따로 만들어서 각자 작업을 완료한 후 이를 master branch에 merge 하여 병합하는 식의 작업을 합니다.** 
   팀원들 각각 독립적이고 서로 영향을 주지 않는 원격 브랜치를 만들어서 본인들이 맡은 부분의 코드를 짜고 master 브랜치에 합치는 식입니다.

어떻게 브랜치를 관리할 것인지에 대한 브랜치 전략은 회사마다 다르지만 이렇게 하는 것이 대부분 일반적 입니다.

* 팀원 본인의 로컬 저장소 master 브랜치 -> 원격으로부터 최신 master원격 브랜치를 pull 해 오고, 자신이 작업한 로컬 브랜치로 이동하여 작업한 후, 자신의 로컬 master 브랜치에 이를 merge시킨 후 이를 다시 원격 master에 반영하는 식으로 사용한다.<br>
   -> 즉, 통합(pull)하여 push하는 용도로 사용합니다.

* 원격 저장소에 있는 단 하나의 master 브랜치 -> 완성해나가는 중인 단 하나의 최종본이라고 생각하면 됩니다. 팀원들은 각자 작업한 것들을 이 master 브랜치에 merge 시켜 나가야 합니다.
<br>

### 관련 용어
---

```
Head
```
Head는 현재 작업 중인 branch를 가리키는 포인터입니다.

```
master
```
git init할 때 자동으로 생성해주는 기본 브랜치
아무런 브랜치도 생성하지 않으면 이 master 브랜치 하나로, 즉 가지 하나로 쭉~ 가는 것입니다
보통 팀원들이 각자의 작업 코드를 하나로 합칠 때 사용하는 뼈대 브랜치로 사용할 수 있습니다.
최종 완성된 배포용 브랜치로 사용할 수도 있습니다.

<br>

### 명령어
---

```
git branch <branch_name>
//새로운 브랜치를 생성합니다. <branch_name>은 생성할 브랜치의 이름입니다.

git branch -d <branch_name>
//특정 브랜치를 삭제합니다. <branch_name>은 삭제할 브랜치의 이름입니다.

git branch -m <old_branch_name> <new_branch_name>
//브랜치의 이름을 변경합니다.

git branch
//로컬 브랜치 목록을 확인합니다. 현재 브랜치는 * 표시로 나타납니다.

git branch -a
//로컬 브랜치와 원격 브랜치 목록을 모두 확인합니다.
```

```
git checkout <branch_name>
//특정 브랜치로 이동합니다. <branch_name>은 이동할 브랜치의 이름입니다.

git checkout -b <branch_name>
// 새로운 브랜치를 생성하고 해당 브랜치로 이동합니다. <branch_name>은 생성할 브랜치의 이름입니다.

git checkout -
//바로 전에 작업하던 브랜치로 이동합니다.
```

### 명령어 사용 예시
---

```
git checkout -b feature/new-feature
// 새로운 기능을 개발할 때, feature 브랜치를 생성하여 작업을 진행합니다.

git checkout -b bugfix/issue-123
// 버그를 수정할 때, bugfix 브랜치를 생성하여 작업을 진행합니다.

git checkout main
git merge feature/new-feature
// 개발이 완료된 기능이나 버그 수정 내용을 main 브랜치에 병합합니다
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}