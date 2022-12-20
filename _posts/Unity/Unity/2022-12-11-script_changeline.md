---
title:  "[Unity] 유니티 스크립트에서 문자열 줄바꾸기"
excerpt: Wrap string in script

categories:
  - Unity
tags:
  - [Unity, 문자열 줄바꿈, Script, Wrap string in script , 스크립트]

toc: true
toc_sticky: true
 
date: 2022-12-12
last_modified_at: 2022-12-12
---

## 개요
매우 신기하게도 유니티에서 일반적으로 줄을 바꿀 때 사용하는 \n을 사용해도 줄바꿈이 되지않습니다.<br>
스크립트에서 텍스트의 줄을 바꿀 때 사용되는 방법 2가지 정도를 소개하고자 합니다.<br>
<br>

## 방법 1
---

가장 쉬우며, string변수 앞에 [TextArea]를 붙여준 뒤 직접 Inspector에서 Enter키로 줄바꿈을 해줍니다.

``` C#
using UnityEngine;
using UnityEngine.UI;

public class testText : MonoBehaviour
{
    [SerializeField] Text _textLine;
    [TextArea] public string _text;  // 인스펙터에서 확인 가능

    void Start()
    {
        _textLine.text = _text;
    }
}
```
<br> 

### 실행 결과
---
![new_line_000](https://user-images.githubusercontent.com/40765022/207053534-bc1d5f65-1b2a-4ab9-8313-1c18ae703242.png)
<br><br>

## 방법 2
---

System.Environment.NewLine 사용하기

``` C#
using UnityEngine;
using UnityEngine.UI;

public class testText : MonoBehaviour
{
    [SerializeField] Text _textLine;

    void Start()
    {
        _textLine.text = "앞" + System.Environment.NewLine + "뒤";
    }
}
```
<br> 

### 실행 결과
---
![new_line_001](https://user-images.githubusercontent.com/40765022/207053536-60d55666-f0dd-4f0b-b81e-b22b54244e41.png)
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}