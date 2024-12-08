---
title:  "[Unity] 유니티 텍스트 크기 자동조정"
excerpt: Unity text size bestfit

categories:
  - Unity
tags:
  - [Unity, text size bestfit, 텍스트 크기 자동조정, 유니티]

toc: true
toc_sticky: true
 
date: 2023-11-20
last_modified_at: 2023-11-20
---

## 텍스트 크기 자동조정
---
유니티에서 텍스트의 크기를 동적으로 조절하여 다양한 화면 크기나 텍스트 길이에 맞춰 레이아웃을 구성하는 것은 매우 중요합니다.<br>
특히 모바일 게임 개발에서는 기기별 화면 크기가 다르기 때문에 텍스트 크기를 자동으로 조절하는 기능은 필수적입니다.<br>
오늘은 간단한 설정으로 텍스트 크기를 자동 조절하는 방법에 대해 알려드리겠습니다.<br>

### 바로 BestFit입니다.

BestFit은 Text 컴포넌트의 속성 중 하나로, 지정된 Rect Transform의 크기에 맞춰 텍스트의 크기를 자동으로 조절하는 기능입니다. <br>
즉, 텍스트가 너무 길어서 Rect Transform 밖으로 벗어나지 않도록 텍스트 크기를 줄이고, 공간이 남으면 텍스트 크기를 키워서 공간을 채울 수 있습니다.<br><br>

물론, 설정된 폰트와 지정 영역에 따른 개행 부분을 완전히 무시하지 않기 때문에 텍스트 데이터의 길이 또는 표시할 텍스트 영역을 조절하고 동작확인할 필요가 있습니다.

---
## 사용 방법
---

![bestfit_00](https://github.com/user-attachments/assets/5fa5a895-16ea-4412-8e46-cd24ece41e43)<br><br>


그 결과 아래와 같이 자동으로 텍스트 글자 크기를 조절해 주는 것을 확인할 수 있습니다.<br><br>

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Unity/Unity/bestfit_01.mp4" type="video/mp4">
</video>

<br>

[Top](#){: .btn .btn--primary }{: .align-right}