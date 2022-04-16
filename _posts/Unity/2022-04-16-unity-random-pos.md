---
title:  "[Unity] GameObject Random Instantiate"
excerpt: Unity에서 랜덤 좌표에 생성 및 좌표 이동

categories:
  - Unity
tags:
  - [Unity, Random Pos, 랜덤 생성, 랜덤 좌표]

toc: true
toc_sticky: true
 
date: 2022-04-16
last_modified_at: 2022-04-16
---

## *개요*
게임 개발에서 랜덤 좌표에 게임오브젝트를 생성해야될 때가 있습니다.(몬스터, 보스의 범위공격 등등)
기초적인 부분이지만 한번 짚고 가도록 하겠습니다.

---
## *순서*
1. 생성할 영역을 지정
2. 좌표를 랜덤으로 지정
3. 지정한 랜덤 좌표에 오브젝트를 생성(이미 생성되있는 오브젝트에 랜덤 좌표 입력)
 
---
### *예제*

---
#### **선언**<br> 
![random_pos_007](https://user-images.githubusercontent.com/40765022/163666142-4a92d50d-45d6-402e-be77-25d494e50825.png)

사용할 오브젝트, 전역변수, 지정영역을 선언 <br>
m_prefab : Prefab화한 게임오브젝트 <br>
m_area : 오브젝트를 생성할 지정영역 <br>
m_random_button : 좌표를 랜덤으로 생성하는 버튼 <br>
m_init_button : 초기화 버튼 <br>
m_count : 몇개의 오브젝트를 생성할것인지를 Editor상의 Component에서 정하기 <br>
m_isExist : 오브젝트가 생성되었는지 아닌지를 판단할 플래그 <br>
m_cubelist : 생성한 오브젝트를 관리할 리스트 <br>
<br>

---
#### **영역 및 랜덤 좌표 지정 부분** <br>
![random_pos_004](https://user-images.githubusercontent.com/40765022/163666106-5fa9c337-2718-46c5-9aa1-8d0d09044e2b.png)


<br>

---
#### **Initialize및 오브젝트 생성 부분** <br>
![random_pos_002](https://user-images.githubusercontent.com/40765022/163665928-6cf2a7fd-562b-46a3-a946-a5cb2488a295.png)

초기화함수에서 버튼을 누르면 실행할 함수를 지정하고 리스트 및 플래그등을 초기화<br>
OnpushRandomButton()함수내에서 생성할때 아래의 지역변수 randonPos 를 선언하지 않고 CalcRandomPos()함수를 Instantiate에 바로 넣어도 상관은 없으나, <br>
가독성의 문제로 지역변수를 선언-> Instantiate에 넣는 방식으로 하였습니다. <br> <br>
![random_pos_002_01](https://user-images.githubusercontent.com/40765022/163666755-6db00262-49d2-46a2-a8a1-e77e1939e9fd.png)
 <br> <br>

---
#### **전체 코드** <br>
![random_pos_001](https://user-images.githubusercontent.com/40765022/163666369-70a9717b-4231-4d39-89bf-c526197965c9.png)


<br>
**[실행 영상]** <br>
<video width="100%" height="100%" controls="controls">
  <source src="assets\images\post\Unity\Unity\random_pos_005.mov" type="video/mov">
</video>



**[초기화버튼 추가]** <br>
<video width="100%" height="100%" controls="controls">
  <source src="assets\images\post\Unity\Unity\random_pos_006.mov" type="video/mov">
</video>




<br>
[Top](#){: .btn .btn--primary }{: .align-right}