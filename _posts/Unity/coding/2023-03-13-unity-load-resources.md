---
title:  "[Unity] 유니티 데이터 또는 리소스(Resources) 로드하기"
excerpt: Unity Load Resources

categories:
  - Unity Code
tags:
  - [Json, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-03-13
last_modified_at: 2023-03-13
---

## 개요
---
유니티에서 이미지 같은 리소스 파일을 로드 하는 방법에 대해서 입니다. <br>
기본적 이며 실무에서 많이 사용하는 방법이니 익혀두시면 도움이 될 것 입니다. <br>

```Resources.Load``` 라는 Unity에서 제공하는 리소스를 로드하는 메소드를 사용하여 로드하는 방식입니다. <br>
여기서 Resources 폴더는 Unity에서 기본적으로 제공되는 폴더 이지만, 처음 유니티를 열었을 때 없을 수도 있으니 그때는 CreateFolder로 Resources폴더를 만들어서 사용하시면 됩니다. <br> <br>

## 사용법
---

```C#

// GameObject Prefab을 로드
GameObject prefab = Resources.Load<GameObject>(“PrefabName”);
// 로드한 Prefab을 인스턴스화
GameObject instantiatedObject = Instantiate(prefab);

// 이미지 Sprite를 로드 하는 방법1 
Sprite spriteImage = Resources.Load<Sprite>("Path + name");
Sprite testImageSprite = spriteImage;

// 이미지 sprite를 로드 하는 방법2
string path = ""illust/stage/" + illustName";
Sprite testImageSprite = Resources.Load<Sprite>(path);
```
<br>

위와같이 매우 간단하게 로드할 수 있습니다.<br>
다만, Resources폴더 내에 많은 리소스를 저장하는것은 매우 좋지않은 방법입니다. <br><br>
왜냐하면 Resources폴더 내에 리소스가 많을 수록 메모리 사용량과 APK,AAB의 용량이 늘어나기 때문입니다. <br>
메모리 사용량과 용량을 줄이기 위해서는 필요한것만 Resources내에 저장하는것이 좋습니다.<br>
(예를들어 Prefab나 BGM데이터 같은 경우 Resources폴더 내에 저장하지 않아도 상관없습니다.)<br><br>

또한 Resources 폴더의 경로는 상대 경로 이기때문에, 폴더 구조가 바뀔 경우 코드가 정상적으로 작동하지 않을 수 있습니다. <br>
이를 방지하기 위해 상대 경로 대신 절대 경로를 사용하는 것이 좋습니다.<br>
<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}