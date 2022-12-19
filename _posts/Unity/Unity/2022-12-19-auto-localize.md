---
title:  "[Unity] 유니티 다국어 지원(Localize)"
excerpt: Auto Localize in Unity

categories:
  - Unity
tags:
  - [Unity, Localize, 로컬라이즈, 유니티]

toc: true
toc_sticky: true
 
date: 2022-12-19
last_modified_at: 2022-12-19
---

## 개요
모바일 어플 또는 게임을 해외판으로 릴리즈 할 때는 해당 국가의 언어로 이름을 바꿀 필요가 있습니다.<br>
해당 국가에 따라 어플의 이름 등을 바꾸는것을 로컬라이즈라고 하는데 오늘은 유니티에서
안드로이드 기준으로 로컬라이즈 하는법을 알아보겠습니다. <br>
IOS에서 로컬라이즈는 유니티가 아닌 XCode에서 해야되는데 이 부분은 추후 포스트 하고 참조링크를 추가하는 방식으로 업데이트 하겠습니다. <br>

---
## 방법
---

먼저 대응할 언어별로 다음과 같이 내용을 적고 ```string.xml``` 파일을 만들어 주세요 <br>
반드시 언어별로 만들어야 합니다. 한국어, 영어 2가지 대응이라면 ```string.xml``` 을 한국어용, 영어용 이렇게 2개를 만들어야 된다는 의미 입니다.<br>

``` xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name"> 어플 이름</string>
</resources>
```

다 되었다면 다음과 같이 언어별 폴더를 만들어 주세요
중국어는 간체 번체 2가지가 있으니 둘다 만들어 줍니다.<br>

```
values-en       // 영어
values-ko       // 한국어
values-ja       // 일본어
values-zh-rCN   // 중국어
values-zh-rTW   // 중국어
```
<br>

![localize_03](https://user-images.githubusercontent.com/40765022/208286790-aa434025-0ac3-4d4a-9ee9-d49edf9f38e0.png) <br><br>

이제 처음 만들었던 각각의 ```string.xml ``` 을 언어별 폴더에 넣어주세요<br>

![localize_02](https://user-images.githubusercontent.com/40765022/208286764-2657dafd-6a92-4e93-b8ff-ee0d57d03c0b.png) <br><br>


마지막 단계입니다.<br>
아래의 유니티 폴더에 상기의 폴더들을 넣어주세요.<br>
만약 Project상에 없다면 Asset아래에 새로 만들어주셔도 무방합니다.<br>

```
Assets\Plugins\Android\res
```
<br>

![localize_00](https://user-images.githubusercontent.com/40765022/208286762-e693892c-f51b-43be-995f-2c0e7c3a9c44.png) <br><br>


![localize_01](https://user-images.githubusercontent.com/40765022/208286763-3a7ad5bb-8b11-4cc2-a00b-abc0c61f2591.png) <br><br>



이제 로컬라이즈 설정이 끝났습니다.<br>
빌드하신 어플을 스마트폰에 설치, 스마트폰의 언어를 변경 하시면 설정하신 해당 언어의 이름으로 변경되는것을 확인 하실 수 있습니다.<br>
<br>

[Top](#){: .btn .btn--primary }{: .align-right}