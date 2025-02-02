---
title:  "[Unity] 유니티 컬러코드Color Code(Hex code)로 텍스트 색상 바꾸는 방법"
excerpt: Color code in Unity Script

categories:
  - Unity
tags:
  - [Unity, Color, ColorCode, HexCode, Script, 컬러코드, 스크립트]

toc: true
toc_sticky: true
 
date: 2022-12-11
last_modified_at: 2022-12-11
---

## 개요
많지는 않지만 Unity상에서 Hex코드를 이용하여 프로그램에서 색을 변경하는경우가 있습니다.<br>
특히 텍스트 1줄내 특정 부분만 색을 변경하여 강조를 한다는 경우도 있으며 이때 Hex코드를 이용하면 간단하게 해결할 수 있습니다.<br>
(+ 텍스트오브젝트를 2개 생성하는 방법도 있습니다. ^^)<br>

자세한 내용은->[Unity Docs](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/StyledText.html)

---
## 사용 방법
---
사용방법으로는 아래와 같이 크게 2가지 정도가 있습니다.
1. 직접 Hex Code를 입력하기 (텍스트내 일부만 색 변경 가능)
2. ColorUtility를 이용하기 (텍스트내 일부만 색 변경 불가)
<br><br>


### 직접 Hex Code를 입력하기
---
``` C#
using UnityEngine;
using UnityEngine.UI;

public class nativesizesample : MonoBehaviour
{
    [SerializeField] Text _result_text;

    void Start()
    {
        _result_text.text = "<color=#ff00ffff>"+ GetClearCount().ToString() + "</color>" + "/" + GetAllStageCount().ToString();
    }
}
```
<br>

#### 실행 결과
---

![color_code_000](https://user-images.githubusercontent.com/40765022/206886614-7da8f384-6c93-4f8d-863b-8cc9a84ca669.png)
<br>
<br>

### ColorUtility를 이용하기
---
``` C#
using UnityEngine;
using UnityEngine.UI;

public class nativesizesample : MonoBehaviour
{
    [SerializeField] Text _result_text;
    private Color _text_color;
    void Start()
    {
        _result_text.text = GetClearCount().ToString() + "/" + GetAllStageCount().ToString();
        _result_text.color = SetColor();
    }

    private Color SetColor()
    {
        ColorUtility.TryParseHtmlString("#008000ff", out _text_color);
        return _text_color;
    }
}
```
<br> 


#### 실행 결과
---
![color_code_001](https://user-images.githubusercontent.com/40765022/206888087-bcdbc7d6-07bb-48dc-98b5-25187d371a6f.png)
<br>


[Top](#){: .btn .btn--primary }{: .align-right}