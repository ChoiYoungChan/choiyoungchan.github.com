---
title:  "[Unity] 자동 이미지 크기 조정"
excerpt: Unity Set Native Size

categories:
  - Unity
tags:
  - [Unity, Set Native Size, 네이티브사이즈, Script, 자동 크기조절, 스크립트]

toc: true
toc_sticky: true
 
date: 2022-12-11
last_modified_at: 2022-12-11
---

## 개요
---
Set Native Size란? <br>
=> 유니티의 이미지 컴포넌트에 기본 탑재된 기능으로 sprite 이미지의 크기로 오브젝트의 크기를 자동으로 조절해주는 기능. <br>

유니티를 처음 시작하시는 분들은 이미지의 크기를 조절하실 때 직접 Rect Transform에서 크기를 조절하시는데 몇개 정도라면 상관없겠지만 복수의 이미지 크기를 조절시 시간도 걸리고
일일히 입력하는것도 일입니다. <br>(+ 간혹 실수해서 이상하게 보이거나 크기조절을 깜빡 잊는 경우도 있습니다.) <br>

이보다 간단히 빨리 크기를 자동으로 조절할 수 있는 방법이 있습니다. <br> <br>

---
## 사용 방법
---
사용방법은 아래와 같이 2가지 정도 있습니다.
1. Editor의 Inspector에서 사용
2. 스크립트에서 사용


### Editor의 Inspector에서 사용
---
아래와 같이 이미지의 sprite image에 해당 이미지를 넣습니다. <br>
![native_size_000](https://user-images.githubusercontent.com/40765022/206886182-273403ab-7ede-40e4-a6a9-b68aca3574db.png)
<br><br>

Preserve Aspect아래부분에 다음과 같이 Set Native Size 버튼이 나오는데 클릭하시면 됩니다.<br>
![native_size_001](https://user-images.githubusercontent.com/40765022/206886184-acfebbed-c42e-4281-b53b-87f886239b0a.png)
<br><br>

아래와 같이 리소스 sprite이미지와 동일한 사이즈로 변경된것을 알 수 있습니다. <br>
![native_size_002](https://user-images.githubusercontent.com/40765022/206886186-ba7f8c16-1edc-4b48-a22b-e6dd377d60ad.png)
<br><br>

### 스크립트에서 사용
---

``` C#
using UnityEngine;
using UnityEngine.UI;

public class nativesizesample : MonoBehaviour
{
    [SerializeField] Image _image;

    void Start()
    {
       // Use Set Native Size in C# Script 
       _image.SetNativeSize();
    }
}
```


<br> 

[Top](#){: .btn .btn--primary }{: .align-right}