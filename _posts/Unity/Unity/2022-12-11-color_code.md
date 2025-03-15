---
title:  "[Unity] 유니티 컬러 코드(Hex code)로 텍스트 색상 변경 완벽 가이드: 쉽고 완벽하게 텍스트 색상 바꾸기"
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

# 유니티 컬러 코드(Hex code)로 텍스트 색상 변경 완벽 가이드: 쉽고 완벽하게 텍스트 색상 바꾸기

유니티에서 텍스트 색상을 변경하는 방법은 다양하지만, 컬러 코드(Hex code)를 사용하면 더욱 정확하고 간편하게 원하는 색상을 적용할 수 있습니다. 이 글에서는 유니티에서 컬러 코드를 사용하여 텍스트 색상을 변경하는 방법을 단계별로 자세히 설명합니다.
자세한 내용은->[Unity Docs](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/StyledText.html)

## 1. 유니티 텍스트 색상 변경 방법

유니티에서 텍스트 색상을 변경하는 방법은 크게 두 가지가 있습니다.

* **유니티 에디터에서 직접 변경**: 유니티 에디터의 Inspector 창에서 텍스트 컴포넌트의 색상을 직접 선택하여 변경합니다.
* **스크립트를 사용하여 변경**: C# 스크립트를 사용하여 텍스트 컴포넌트의 색상을 프로그래밍 방식으로 변경합니다.

## 2. 컬러 코드(Hex code)란 무엇인가?

컬러 코드는 빨간색(R), 녹색(G), 파란색(B)의 조합을 16진수로 표현한 색상 코드입니다. 웹 디자인, 그래픽 디자인 등 다양한 분야에서 사용되며, 유니티에서도 텍스트 색상을 정확하게 지정하는 데 유용합니다.

* 예시: 흰색(#FFFFFF), 검은색(#000000), 빨간색(#FF0000)

## 3. 유니티 에디터에서 컬러 코드로 텍스트 색상 변경

1.  유니티 에디터를 실행하고 텍스트 컴포넌트가 포함된 게임 오브젝트를 선택합니다.
2.  Inspector 창에서 텍스트 컴포넌트(Text, TextMeshPro 등)를 찾습니다.
3.  Color 속성을 클릭하여 색상 선택 창을 엽니다.
4.  색상 선택 창 하단의 Hex 입력란에 원하는 컬러 코드를 입력하고 Enter 키를 누릅니다. [컬러 코드 입력 이미지 필요 합니다]

## 4. 스크립트를 사용하여 컬러 코드로 텍스트 색상 변경

1.  유니티 에디터를 실행하고 텍스트 컴포넌트가 포함된 게임 오브젝트에 C# 스크립트를 추가합니다.
2.  스크립트를 열고 다음과 같이 코드를 작성합니다.

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

### 실행 결과
---

![color_code_000](https://user-images.githubusercontent.com/40765022/206886614-7da8f384-6c93-4f8d-863b-8cc9a84ca669.png)
<br><br>

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

### 실행 결과
---
![color_code_001](https://user-images.githubusercontent.com/40765022/206888087-bcdbc7d6-07bb-48dc-98b5-25187d371a6f.png)
<br>

## 5. TextMeshPro 사용 시 주의사항

TextMeshPro를 사용하는 경우, `UnityEngine.UI.Text` 대신 `TMPro.TextMeshProUGUI` 또는 `TMPro.TextMeshPro` 컴포넌트를 사용해야 합니다. 또한, `using TMPro;` 네임스페이스를 추가해야 합니다.

## 6. 추가 정보

* **컬러 코드 생성**: 온라인 컬러 코드 생성 도구를 사용하여 다양한 색상의 컬러 코드를 얻을 수 있습니다.
* **ColorUtility 클래스**: `ColorUtility.TryParseHtmlString()` 함수를 사용하여 컬러 코드를 Color 객체로 변환할 수 있습니다.
* **TextMeshPro**: 고품질 텍스트 렌더링을 위한 유니티 에셋입니다.

유니티에서 컬러 코드를 사용하여 텍스트 색상을 변경하는 방법을 익히면 더욱 다양하고 세밀한 텍스트 표현이 가능합니다.
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}