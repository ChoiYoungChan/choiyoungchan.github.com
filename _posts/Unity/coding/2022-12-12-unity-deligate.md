---
title:  "[Unity] 유니티 델리게이트"
excerpt: delegate in Unity

categories:
  - Unity Code
tags:
  - [Programming, Unity, delegate, 델리게이트, 유니티]

toc: true
toc_sticky: true
 
date: 2022-12-12
last_modified_at: 2022-12-12
---

## Deligate의 개념
---
델리게이트란 함수를 변수처럼 사용할 수 있는것 입니다.<br>
자세한 설명은 ->[C#-Delegate](https://choiyoungchan.github.io/c%20sharp/deligate/)<br>

유니티에서 델리게이트를 사용하는 방법에 관하여, 집중적으로 설명하고자 합니다.<br>
유니티에서 델리게이트를 사용하는데에는 2가지가 있으며, 여기서 델리게이트를 더 편하게 사용가능한 기능은 3가지가 있습니다.<br><br>

유니티에서 델리게이트 사용방법
1. C#과 동일하게 델리게이트를 사용
2. UnityAction
<br>

더 편하게 사용가능한 기능
1. Anonymous method
2. Lambda
3. Action과 Func
<br><br>

### Anonymous method(익명 또는 이름없는 Method)
Method의 몸체(내용)만 있는 Method를 말하며, 이 익명의 Method를 델리게이트에 사용할 수 있습니다.<br>
단순히 Method명 대신 아래와 같이 delegate키워드와 함께 익명 Method의 형태를 넣으면 됩니다.<br>

```c#
delegate(매개변수) { 내용; };
```

### Lambda(람다식)
상기의 익명의 Method 보다 간단하게 람다식으로도 가능하며 아래와 같이 사용할 수 있습니다.<br>
( ()=> 부분 입니다.)<br>

```c#
test_delegate _test = (x, y) => x + y;
```
<br>

### Action과 Func
Action과Func는 유니티에서 미리 정의된 델리게이트 타입으로 델맄게이트를 정의하지 않고 바로 델리게이트 변수를 만들 수 있습니다.<br>
이를 사용하기 위해서는 System네임스페이스를 사용해야 합니다. 
<br>
Action : 반환값이 없는 델리게이트
Func : 반환값이 있느 델리게이트

#### Action을 이용한 방법
```c#
 Action _testAction = ShowLog;
 _testAction();
```
<br>

#### Func를 이용한 방법
Func의 경우 인수와 반환 타입 모두 제네릭 표시를 해야 되기 때문에 순서에 맞게 적는것이 중요합니다.<br>
<인수1, 반환타입>처럼 반환타입을 마지막에 적어야 됩니다.<br>

```c#
Func<int, string> _testFunc = AddNumber;
Debug.Log(_testFunc(10));
```


<br>

## 사용 방법
---

### 미리 정의된 Method를 전달하는 델리게이트

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    delegate void delegateTest();
    delegateTest _delegateTest;

    // Start is called before the first frame update
    void Start()
    {
        //_delegateTest = ShowText;
        _delegateTest = ShowLog;
        _delegateTest();
    }

    void ShowLog()
    {
        Debug.LogError("Delegate Test Log");
    }
}
```


### Anonymous method(익명 또는 이름없는 Method)

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    delegate void delegateTest();
    // Start is called before the first frame update
    void Start()
    {
        delegateTest _delegateTest = delegate ()
        {
            Debug.Log("Delegate Test Log");;
        };
        _delegateTest();
    }
}
```

### Lambda(람다식)

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    delegate void delegateTest();
    delegateTest _delegateTest;

    // Start is called before the first frame update
    void Start()
    {
        //_delegateTest = ShowText;
        _delegateTest = () => Debug.Log("Delegate Test Log");
        _delegateTest();
    }
}
```

### Action과 Func

#### Action

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Action _testAction = ShowLog;
        _testAction();
    }

    void ShowLog()
    {
        Debug.Log("Action Test Log");
    }
}
```

Action 에서 람다식 이용

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Action _testAction = () => Debug.Log("Action Test Log");
        _testAction();
    }
}
```



#### Func

```c#
using System;
using UnityEngine;
using UnityEngine.UI;

public class TestDelegate : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Func<int, string> _testFunc = AddNumber;
        Debug.Log(_testFunc(10));
    }

    string AddNumber(int _number)
    {
        return $"출력 : {_number}";
    }
}
```

<br>


[Top](#){: .btn .btn--primary }{: .align-right}