---
title:  "[Unity] 유니티 PlayerPref 데이터 저장 및 사용"
excerpt: playerpref in Unity

categories:
  - Unity Code
tags:
  - [Unity, 유니티, PlayerPref]

toc: true
toc_sticky: true
 
date: 2022-12-23
last_modified_at: 2022-12-23
---

## 개요
---
유니티 내에서 간단한 수치나 게임데이터 등을 저장해야할 필요성이 있을 때가 있습니다.
특히 게임 내 진행 스테이지, 게임머니, 게임 데이터 등등이 있습니다.
이러한 데이터를 저장하지 않을 경우 유니티를 재가동 했을 경우 도중부터가 아닌 처음부터 시작하는것 을 볼 수 있습니다.

게임데이터 등을 저장할 때 사용하는것이 PlayerPrefs라는 기능입니다.

## 사용법
---
<br>

PlayerPref에 값을 설정 및 저장하는 방법은 아래와 같습니다. <br>
```c#
PlayerPrefs.SetInt("Key_Name", int_Value); // int 값을 저장
PlayerPrefs.SetFloat("Key_Name", float_Value); // float 값을 저장
PlayerPrefs.SetString("Key_Name", string_Value); // string 값을 저장
PlayerPrefs.Save() // 값을 저장
```
<br>

저장된 PlayerPrefs데이터를 불러올 떄는 아래와 같이 저장시 지정한 key를 이용해 불러올 수 있습니다. <br>
```c#
int int_Value = PlayerPrefs.GetInt("Key_Name");
float float_Value = PlayerPrefs.GetFloat("Key_Name");
string string_Value = PlayerPrefs.GetString("Key_Name");
```

<br>

저장된 PlayerPrefs데이터를 삭제 하고 싶을 때는 2가 방법이 있습니다. <br>
1. 아래의 방식의 코드를 이용하여 삭제하기
2. Unity의 메뉴에서 삭제하기

<br>

먼저 코드상에서 PlayerPrefs데이터를 삭제하는 방법은 아래와 같습니다. <br>
```c#
PlayerPrefs.DeleteAll();    // 모두 삭제하기
PlayerPrefs.DeleteKey("Key_Name"); // key 삭제하기
```
<br>

유니티 상에서 삭제하는 방법은 아래와 같이 유니티 메뉴 Edit ->Clear all PlayerPrefs 버튼을 눌러 삭제할 수 있습니다. <br>

![playerprefs_000](https://user-images.githubusercontent.com/40765022/209464806-acec0f19-3f76-4d93-8d63-dfd052b5d26d.png)

(버튼의 위치는 유니티 버전에 따라 다를 수 있습니다. 상기의 유니티 버전은 2021.3.8f1)  <br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}