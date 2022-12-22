---
title:  "[Git] .gitignore(무시할 파일 목록)을 만드는법"
excerpt: .gitignore(무시할 파일 목록)을 만드는법에 관하여

categories:
  - Git
tags:
  - [Github, Git, .gitignore]

toc: true
toc_sticky: true
 
date: 2022-01-10
last_modified_at: 2022-01-10
---


## .gitignore이란?
---
GitHub의 원격 리포지토리에 로컬 리포지토리의 작업내용, 프로젝트를 올릴때 불필요한 파일들(로그파일, 유니티등 에디터 기본제공 라이브러리 등등)은 <u>올리지 않고 무시할 파일들 목록이 적힌 파일</u>

---

## .gitignor만들기
---
만드는 방법은 크게 3가지가 있다.
1. GitHub에서 리포지토리를 만들때 생성하는것
2. 터미널에서 생성하는것
3. 외부 사이트에서 생성하는것
 
 <br>

### GitHub에서 리포지토리를 만들때 생성하는법 <br>

* 다음과 같이 리포지토리를 생성할 시에 ```.gitignore```파일을 만들 수 있다. <br> 
'.gitignore template' 에서 유니티, UE4 같은 에디터의 템플렛을 설정할경우 해당 에디터나 템플렛의 기본 제공 라이브러리나 로그파일이 자동으로 gitignore파일에 작성된 상태로 생성이 된다. <br> 
![gitignore_000](https://user-images.githubusercontent.com/40765022/148752883-c7697b8c-3fd4-4157-ab96-ad8b50be26c2.png)
<br> 
<br> 

### 터미널에서 생성하는법 <br>
* git프로젝트의 디렉터리에 들어가서 Git bash를 연 다음 아래의 명령어를 실행함으로서 ```.gitignore```파일을 생성할 수 있다. <br> 
![gitignore_001](https://user-images.githubusercontent.com/40765022/148751318-a65f38e7-5eb2-4716-81c1-3ce30930041c.png) <br> 
 <br> 
![gitignore_002](https://user-images.githubusercontent.com/40765022/148751360-d89b749a-b9dd-4c8b-b2db-59960038cee1.png) <br> 
생성된 ```.gitignore```파일 <br> 
 <br> 

### 외부 사이트에서 생성하는법 <br>

[GitIgnore.io](https://www.toptal.com/developers/gitignore) <br> <br>
위의 사이트에 들어가서 프로젝트 언어, 에디터, 툴 별로 ```.gitignore```에 추가할 목록들을 생성할 수 있다. <br> <br>

![gitignore_003](https://user-images.githubusercontent.com/40765022/148751396-7af81d8b-41c3-4425-9444-cc7902121db6.png) <br>
<br>
만약 Unity와 php 등등을 사용하는 경우 검색, 추가한 후 생성 버튼을 눌러주면 된다. <br>
그러면 텍스트들이 나오는데 복사하여 ```.gitignore```에 붙여넣으면된다.



---
## .gitignore적용하기  <br>
---
아래의 코드를 이용하여 ```.gitignore``` 파일을 push해서 적용해주면 된다. <br>

```
$ git add .gitignore
$ git commit -m "commit message" 
$ git push
```

---

<br>
[Top](#){: .btn .btn--primary }{: .align-right}