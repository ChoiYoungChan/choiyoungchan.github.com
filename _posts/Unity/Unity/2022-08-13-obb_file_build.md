---
title:  "[Unity] 유니티에서 Obb파일 빌드하기"
excerpt: build Obb file at Unity

categories:
  - Unity
tags:
  - [Unity, Obb]

toc: true
toc_sticky: true
 
date: 2022-08-13
last_modified_at: 2022-08-13
---

## 개요
기본적으로 Google Play스토어에 업로드할 앱은 Apk, Aab를 주로 업로드 해서 릴리즈 하는방식입니다. <br>
다만, Google Play 스토어에는 100~150MB의 용량 제한이 있어 가급적 100MB전후가 되어야만 합니다.<br>

앱이 용량 제한을 초과하는 경우(이는 대형 게임의 경우 매우 흔합니다.)<br>
출력 패키지를 메인 부분(Apk)과 확장 파일(Obb)로 나누어서 Apk를 최소 용량으로, 기타 리소스 파일들은 Obb에, 라는 식이 됩니다.
<br>
(물론 이는 앱 패키지를 나누는 유일한 방법이 아닌, 에셋 번들과 서드 파티 플러그인을 추가하여 다른 분할 빌드하는 법 또한 많이 존재합니다.)

자세한 내용은->[Andrroid 개발자 문서](https://developer.android.com/google/play/expansion-files)

---
## 빌드 방법
---
Unity에서 앱 출력 패키지를 Apk와 Obb로 분할하게 하려면아래의 순서대로 하면 됩니다. (간단합니다.)

1. PlayerSettings에서 Publishing Settings패널을 선택, 연다
<br>

![obb_0000](https://user-images.githubusercontent.com/40765022/184476664-c7f6b801-c3c8-4e71-a6d9-8a51ccac012d.png) <br>
![obb_0001](https://user-images.githubusercontent.com/40765022/184476665-6247457a-f5ac-43fe-aef3-f35eeacedb68.png) <br>


<br>

2. Publishing Settings패널 내에 있는 Split Application Binary를 체크하여 활성화 합니다.
<br>

![obb_0002](https://user-images.githubusercontent.com/40765022/184476666-a8fa723a-450e-4447-8d11-bc4b9703510a.png)

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}