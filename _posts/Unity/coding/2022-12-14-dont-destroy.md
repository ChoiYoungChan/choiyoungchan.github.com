---
title:  "[Unity] 파괴하지 않을 게임 오브젝트 만들기"
excerpt: Don't Destroy On Land

categories:
  - Unity Code
tags:
  - [Don't Destroy, Unity, 안없어지는, 오브젝트, 유니티]

toc: true
toc_sticky: true
 
date: 2022-12-14
last_modified_at: 2022-12-14
---

## 개요
---
기본적으로 유니티는 씬(Scene) 단위로 공간 또는 장소를 구현하며,<br>
다른 Scene으로 이동할 때는 기존의 Scene이 언로드 되는 동시에 기존 Scene의 오브젝트 들이 없어집니다.<br>
하지만 설계 또는 개발자의 의도 등으로 다른 Scene으로 이동하더라도 기존 Scene의 오브젝트가 없어지지 않도록 설정할 필요가 있습니다. <br>
이때 사용하는것이 DontDestroyOnLoad입니다. <br>



## 사용법
---

사용방법은 매우 간단하며, 아래와 같이 DontDestroyOnLand를 사용하시면 됩니다.

``` C#
public class DontDestoryObject : MonoBehaviour
{
    private void Awake()
    {
        DontDestroyOnLoad(gameObject);
    }
}
```


단, 이동한 2번째 Scene에서 다시 기존 Scene으로 돌아왔다가 다시 다음 Scene으로 이동 한다면 없어지지 않고 남아있는 오브젝트가 계속 누적되어갈 것입니다. <br>
이는 메모리의 사용량을 증가시키고 작동문제(버그)가 발생할 가능성이 매우 높아집니다. <br>
이에 대한 해결 방법은 3가지가 있습니다.

1. 중복되는 오브젝트인지 먼저 확인후 없애기 또는 DontDestroyOnLoad처리
2. 초기화용 Scene을 만들기
3. 라이프 사이클 만들기

<br>
첫번째 방법 입니다. <br>
코드상에서 중복되는 오브젝트인지 먼저 확인후 없애기 또는 DontDestroyOnLoad처리를 해줍니다. <br>

``` C#
public class DontDestoryObject : MonoBehaviour
{
    private void Awake()
    {
        var obj = FindObjectsOfType<DontDestoryObject>();
        if (obj.Length == 1) {
            DontDestroyOnLoad(gameObject);
        } else {
            Destroy(gameObject);
        }
    }
}
```
<br>

두번째 방법 입니다. <br>
없애지 않을 게임 오브젝트를 생성하는 전용 Scene을 만들어 그 Scene에서 생성한 뒤 다른 씬만 오가는 방식입니다.<br>
이 방법 게임 내에서 단 하나만 존재하는 오브젝트를 만들고자 하는 경우에 유용한 방법입니다.<br>

![dontdestroyonload_000](https://user-images.githubusercontent.com/40765022/207613269-2d76367e-c33b-4dff-8ed5-e11fd5baa187.png) <br><br>


세번째 방법 입니다. <br>
상기의 2가지 방법은 1개의 오브젝트일때 유용하지만 여러개일 경우 적절하지 않습니다. <br>
만약 복수의 오브젝를 없애지 않는 처리를 한다면 Scene 배치 방식 보다 Prefab으로 관리하고 필요한 시점에 생성하게 하는것이 편하다. <br>
이 경우 생성, 불필요시 없애는 라이프 사이클의 관리가 필요하다. <br>
![dontdestroyonload_001](https://user-images.githubusercontent.com/40765022/207613273-d022ee4b-75c5-4688-9598-1e142b6d859f.png) <br><br>

<br>
[Top](#){: .btn .btn--primary }{: .align-right}