---
title:  "[Git] 깃 명령어 Git Command 정리"
excerpt: Git 명령어 정리

categories:
  - Git
tags:
  - [Github, Git]

toc: true
toc_sticky: true
 
date: 2022-01-10
last_modified_at: 2022-01-10
---


## Git 명령어 <br>
---
---

### 최초 설정 명령어 <br>
---

```
$ git init
```
- 현재 디렉토리를 로컬 리포지토리로 지정
- ls -al 명령어로 .git 숨김파일 생성을 확인
 <br>

```
$ git config --global user.name "XXXX"
```
- git 계정명 등록 <br>
 <br>

```
$ git config --global user.email "XXXX@XXXX.com"
```
- git 이메일등록 <br>
 <br>

```
$ git config --list 
```
- git 설정정보 조회 <br>
 <br>


### 기본 명령어 <br>
---

```
$ git remote
$ git remote -v         # -v 옵션을 주면 단축이름과 URL을 함께 볼 수 있다.
```
- 현재 등록된 원격 리포지토리를 확인할 수 있다. <br>
 <br>

```
$ git status
```
- 파일의 상태를 확인 <br>
 <br>

```
$ git clone https://github.com/XXXX/XXXXXX.git
```
원격 리포지토리를 로컬로 복제하는것 <br>
 <br>

 ```
$ git add <파일/디렉토리 경로>   # 변경 내용의 추가하고 싶을 때 경로를 인자로 넘긴다.
$ git add .                     # 현재 폴더의 전체 파일을 이동
$ git add -p                    # 각 변경 사항을 터미널에서 직접 눈으로 확인하면서
                                  스테이징 영역으로 넘기거나 또는 제외
```
변경내용을 스테이징 영역에 추가(커밋 하기 위해)하기 위해 사용 <br>
 <br>


```
$ git commit -m "커밋 메시지"               # 커밋 메시지 작성
$ git commit --amend "새 커밋 메시지"       # 커밋 메시지 수정
```
- 커밋 메시지 작성/수정 <br>
 <br>

```
$ git push <저장소명> <Branch명>
$ git push -u origin master
```
- 원격 리포지토리에 로컬에서 커밋 한 작업내용을 올림
- u 옵션을 사용하면 최초 한 번만 저장소명과 Branch명을 입력하고 이후에 생략 가능하다. <br>
 <br>


```
$ git fetch
```
- 원격 리포지토리로 부터 변경된 내용을 가지고 온 후 병합(merge) x
- 변경된 내역을 가지고 온 후 검토 후에 merge 할 수 있어서 충돌 방지 <br>
 <br>


```
$ git merge <Branch명>
$ git merge origin/master
```
- Branch를 병합하는 명령어
- 협동 프로젝트 과정에서 같은 이름의 파일 안에 수정한 부분이 겹칠 때 충돌(conflit)이 발생 할 수 있다. <br>
 <br>


```
$ git pull
```
- 원격 리포지토리로 부터 변경된 내용을 가지고 온 후 병합(merge)
- pull = fetch + merge <br>
 <br>


### Branch 명령어 <br>
---

```
$ git branch <Branch명>
```
- <Branch명> 이라는 Branch를 생성하는 명령어 <br>
 <br>


```
$ git checkout <Branch명>
$ git checkout <파일 위치>              # 해당 파일 혹은 위치의 모든 파일의 변경사항을 없앰
```
- 현재 master Branch에서 <Branch명> 으로 이동하기 위한 명령어
- b 옵션을 사용하면 Branch 생성과 체크아웃을 한번에 할 수 있다. <br>
 <br>

```
$ git branch -m <이전 Branch명> <새 Branch명>
```
- Branch 이름 변경 <br>
 <br>


```
$ git branch -d <Branch명>
```
-  <Branch명> 삭제 <br>
 <br>


```
$ git branch -a
```
- 모든 Branch 확인 <br>
 <br>

---


### 알아두면 좋은 Git 명령어 <br>
--- 
---
<br>

```
$ git add -f <파일 명>
```
- .gitignore를 무시하고 추가하기 <br>
 <br>

 ```
$ git stash
```
- 파일의 변경 사항을 전부 임시 저장함에 저장, 나중에 다시 꺼내와 마무리할 수 있다.
 <br>


```
$ git diff                                      # 커밋된 파일과 현재 파일을 비교
$ git diff --staged                             # 커밋된 파일과 add된 파일을 비교         
$ git diff HEAD HEAD^                           # 가장 최근의 커미과 그 전의 커밋을 비교
$ git diff [비교할branch1] [비교할branch2]       # Branch간의 비교  
```
- 파일의 어떤 내용이 변경 되었는지 차이점을 비교할 수 있다.
- 로컬 리포지토리와 스테이징 과 비교, 커밋이나 Branch간의 비교도 가능하다. <br>
 <br>


```
$ git log
```
- commit의 변경 내역 보기 <br>
 <br>


```
$ git rebase <Branch명>
```
- Branch 리베이스
- Branch를 병합하는 명령어로 merge와 같은 기능이지만, <br>
  merge의 경우 병합 할 Branch에서 기록한 모든 commit이 master의 commit으로 기록된다. <br> 
 <br> 


```
$ git rm -f  <파일명>
```
- 해당파일 삭제 <br>
 <br>


## 참고 문헌

[Git명령어 모음](https://khs613.github.io/github/github-base/) <br>
[Atlassian](https://www.atlassian.com/git/glossary) <br>
[Snow System](https://snowsystem.net/git/git-command/git-rm/#) <br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}