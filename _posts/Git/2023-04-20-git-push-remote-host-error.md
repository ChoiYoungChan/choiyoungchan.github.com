---
title:  "[Git] git push WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! 에러"
excerpt: fix git push WARNING REMOTE HOST IDENTIFICATION HAS CHANGED! error

categories:
  - Git
tags:
  - [Github, Git, git REMOTE HOST errㅐr, 깃, 원격 호스트 에러]

toc: true
toc_sticky: true
 
date: 2023-04-20
last_modified_at: 2023-04-20
---


## 개요 및 발생 원인
---
SSH에서는 처음 접속시에 접속처 호스트의 공개키를 보존해 두고, 다음에 접속시에 호스트키를 비교해 전회와 같은 호스트에 접속했는지를 확인하는 구조로 되어 있습니다. <br>
때문에, IP 주소의 재설정이나 OS 재설치 등으로 호스트 키가 바뀌어 버렸을 경우, 다음과 같은 에러 메세지가 나와 SSH 접속이 실패해 버립니다.<br>

최근 이라기에는 1달 넘게 지났지만 GitHub에서 새로운 RSA SSH 호스트 키를 업데이트 하면서 아마 대부분 Push할때 아래의 에러가 나왔을 겁니다.<br>

[GitHub SSH Issue](https://github.blog/2023-03-23-we-updated-our-rsa-ssh-host-key/)

<br>

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@  WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!   @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:u--tksC-----QXVU--cz--Cvj-----s.
Please contact your system administrator.
Add correct host key in /Users/choi/.ssh/known_hosts to get rid of this message.
Offending RSA key in /Users/choi/.ssh/known_hosts:1
Host key for github.com has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
<br>

## 해결 방법
---

이에 대한 해결책은 매우 간단한데, 바로 known_host에 올바른 호스트 키를 추가하여 올바른 액세스 권한과 리포지토리의 존재를 확인시키면 됩니다.<br>
순서로는 아래와 같습니다.<br>
1. .ssh/known_host에서 ```github.com``` 호스트 정보 삭제
2. 다시 github에 ssh연결 (중간에 선택이 나온다면 yes로 답변)
3. git push 시도하여 성공하면 문제 해결

<br>

### 1 .ssh/known_host에서 ```github.com``` 호스트 정보 삭제

 $HOME/.ssh/known_hosts해당 행을 에디터에서 삭제해도 됩니다만, 아래와 같이 명령의 ssh-keygen옵션 -R으로 지울 수도 있습니다.

```
$ssh-keygen -R example.com
# Host example.com found: line 133 type RSA
/Users/hnw/.ssh/known_hosts updated.
Original contents retained as /Users/hnw/.ssh/known_hosts.old
```
<br>

### 2 다시 github에 ssh연결 (중간에 선택이 나온다면 yes로 답변)

```
% ssh -T git@github.com
The authenticity of host 'github.com (xxx.xxx.xxx.xxx)' can't be established.
XX00000 key fingerprint is SHA256: xxxx
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes 
Warning: Permanently added 'github.com' (XX00000) to the list of known hosts.
Hi user! You've successfully authenticated, but GitHub does not provide shell access.
```
<br>

### 3 git push 시도하여 성공하면 문제 해결

<br><br><br>

### 상기의 해결책을 사용해도 계속 반복되는 경우(여러 번 SSH키 변경이 발생하는 경우)
---
OS 설치를 반복하는 등의 이유로 특정 호스트의 호스트 키가 매번 바뀌는 상황에서는 위 명령을 치는 것조차 번거로울 수 있습니다.<br>
이 경우 다음과 같은 $HOME/.ssh/config설정으로 호스트 키 검사를 비활성화 할 수 있습니다.<br>

```
Host 192.168.1.1
StrictHostKeyChecking no
UserKnownHostsFile /dev/null
```
말할 필요도 없지만 모든 호스트에 대해 이 설정을 구성하면 중간자 공격에 취약해집니다. <br>
필요할 때만 특정 호스트만 설정해야 합니다. <br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}