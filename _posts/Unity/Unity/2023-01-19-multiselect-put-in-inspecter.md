---
title:  "[Unity] 유니티 여러개 오브젝트 또는 데이터를 인스펙터에 동시에 넣기"
excerpt: put multi select object in inspecter

categories:
  - Unity
tags:
  - [Unity, multi select, one time, 유니티, 여러개 동시게 넣기]

toc: true
toc_sticky: true
 
date: 2023-01-19
last_modified_at: 2023-01-19
---

## 개요

유용한 기능중 한가지 입니다. 코드 인스펙터에서 배열 형태로 오브젝트 또는 sprite등의 데이터 등을 지정할때 일일히 배열에 넣는것이 매우 비효율적이기에 사용하는 방법입니다.
새로운 방법이나 신기술이 아닌 기존의 기술이지만 모르시거나 사용해본적이 없었던 방식일 수도 있기 때문에 이런 방법도 있으니 실무나 학습때 유용할것이라 판단됩니다.

---
## 방법
---

많은 분들이 아래와 같이 복수의 sprite나 gameObject, Prefab등을 배열 형식으로 지정, 인스펙터를 통해 스크립트와 연결할 수 있다는것을 알고 계실 것 입니다.

```C#
#region private
[SerializeField] Sprite[] _sprites;
```

상기와 같이 Sprite[]형식으로 할 경우 유니티의 인스펙터 상에서는 아래와 같이 표시가되어 복수의 오브젝트를 추가할 수 있게 됩니다. <br>

![multi_select_00](https://user-images.githubusercontent.com/40765022/211181182-4bd616c8-1f2a-4a26-8395-9d7a0969032d.png)

<br>

여기서부터 중요한 부분인데 인스펙서 창의 오른쪽 상단을 보시면 아래와 같이 자물쇠 표시가 되어있습니다.
![multi_select_01](https://user-images.githubusercontent.com/40765022/211181181-f930e08c-fbbc-4eb4-9e06-ced5a44785fb.png)

<br>

이 버튼은 현재 보고 있는 인스펙터 창을 고정하여 다른 오브젝트나 project내 다른것을 선택하더라도 선택한 것의 정보가 아닌 고정된 인스펙터 창을 보여주는 역할을 합니다. <br>

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Unity/Unity/multi_select_00.mp4" type="video/mp4">
</video>

<br><br>
이제 제가 다음엔 어떻게 하는지 짐작 되시는 분들도 계실겁니다. <br>
다음 동영상과 같이 여러 오브젝트를 넣고자 하는 오브젝트의 인스펙터 창을 고정한 후, <br>
넣어줄 복수의 오브젝트를 선택하여 한번에 드래그 앤 드롭으로 넣어주기만 하면 됩니다. <br>

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Unity/Unity/multi_select_01.mp4" type="video/mp4">
</video>


<br>

[Top](#){: .btn .btn--primary }{: .align-right}