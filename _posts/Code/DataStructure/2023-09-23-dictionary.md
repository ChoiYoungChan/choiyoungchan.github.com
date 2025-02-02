---
title:  "[Data Structure] 딕셔너리(Dictionary)"
excerpt: Dictionary

categories:
  - Data Structure
tags:
  - [datastructure, 딕셔너리, Dictionary]

toc: true
toc_sticky: true
 
date: 2023-09-23
last_modified_at: 2023-09-23
---

## Dictionary 란?
---
해시맵과 동일하게 키-값 쌍으로 데이터를 저장하는 비선형 자료구조이며, ‘키’를 이용하여 데이터를 빠르게 검색할 수 있습니다. <br>
Hash Map과 동일하게 기본적인 자료구조로서 키를 사용하고 키와 값의 타입에 제한이 없으며 동기화 되지 않는다는 공통점이 있습니다. <br> <br>
다만, Hash Map이 Dictionary보다 빠르고 Dictionary는 C# 8.0 이상 부터 사용 가능하고 Hash Map은 그 이전버전 까지만 사용 가능하다는 점 입니다. <br>
그냥 한마디로 정의하자면, Dictionary는 Hash Map의 후속버전이라 생각하시면 편합니다.


### 해시맵(Hash Map)과 차이점

1. 버전
   - Dictionary : C# 8.0 이상 부터 사용 가능
   - Hash Map   : C# 8.0 이전 까지 사용 가능

2. 속도
   - Dictionary : Hash Map보다 느림
   - Hash Map   : Dictionary보다 빠름

<br>

[Hash Map 포스트]()<br><br>



## 사용하는 이유
---
- 키를 이용하여 데이터를 빠르게 검색할 수 있습니다.
- 데이터의 저장 및 검색이 효율적입니다.
- 데이터의 중복을 허용하지 않습니다.


## 문제점&주의사항
---
- 키의 범위가 넓을 경우 해시 충돌이 발생할 수 있습니다.
- 해시 충돌을 해결하기 위해 별도의 자료구조를 사용해야 할 수 있습니다.


## 예제
---

```C#
using System;
using System.Collections.Generic;

class Dictionary
{
    static void Main(string[] args)
    {
        Dictionary<string, int> _dictionary = new Dictionary<string, int>();

        // Dictionary에 데이터를 추가합니다.
        _dictionary.Add("pen", 1);
        _dictionary.Add("eraser", 2);
        _dictionary.Add("sharp pencil", 3);

        // Dictionary에서 데이터를 검색합니다.
        int value = _dictionary["pen"];
        Console.WriteLine(value);

        // Dictionary에서 데이터를 삭제합니다.
        _dictionary.Remove("pen");
    }
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}