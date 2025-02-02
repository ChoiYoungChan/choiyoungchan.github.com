---
title:  "[C#] 더 이상 사용하지 않거나 그럴 예정인 코드에 대해서(Attribute:Obsolete)"
excerpt: Obsolete

categories:
  - C Sharp
tags:
  - [C#, Attribute:Obsolete, 사용하지 않는 코드, 사용하지 않을 예정인 코드]

toc: true
toc_sticky: true
 
date: 2024-09-05
last_modified_at: 2024-09-05
---

## 개요
---
C#에서 Obsolete 속성은 더 이상 사용하지 않거나 권장하지 않는 코드 부분에 붙여 사용하는 속성입니다. <br>
컴파일러는 이 속성이 붙은 멤버(메서드, 클래스, 필드 등)에 접근하려고 할 때 경고 또는 오류 메시지를 출력하여 개발자가 더 적절한 대체 방법을 사용하도록 유도합니다.<br><br>

### 주요 목적
---
* 코드 유지보수: 더 이상 사용되지 않는 코드를 명확하게 표시하여 코드베이스를 정리하고 유지보수를 용이하게 합니다.
* 미래 호환성: 새로운 버전에서 제거될 예정인 기능을 미리 알리고, 개발자가 새로운 기능으로 마이그레이션하도록 안내합니다.
* 코드 품질 향상: 더 나은 대체 방법을 제시하여 코드 품질을 향상시킵니다.<br><br>

---
### 장단점
---
#### 장점
* 명확한 의도 표현: 코드를 사용하지 않도록 명확하게 의도를 전달합니다.
* 코드 유지보수 용이: 더 이상 사용되지 않는 코드를 쉽게 식별하고 제거할 수 있습니다.
* 미래 호환성 보장: 새로운 버전에서 코드가 변경될 때 발생할 수 있는 문제를 미리 방지합니다.<br>

#### 단점
* 코드 복잡성 증가: 많은 Obsolete 속성을 사용하면 코드가 복잡해 보일 수 있습니다.
* 기존 코드와의 호환성 문제: 기존 코드를 수정하지 않고 계속 사용해야 하는 경우 문제가 발생할 수 있습니다.<br><br>


### 주의사항
---
* 적절한 시기에 사용: 새로운 기능이 추가되거나 기존 기능이 변경될 때 적절한 시기에 Obsolete 속성을 적용해야 합니다.
* 명확한 대체 방법 제시: Obsolete 메시지에 대체 방법을 명확하게 제시해야 합니다.
* 점진적인 제거: 기존 코드와의 호환성을 고려하여 점진적으로 Obsolete 메서드를 제거하는 것이 좋습니다.<br><br>


## 사용 예시
---

```c#
[Obsolete("Use the new CalculateArea(double radius) method instead.", true)]
public double CalculateCircleArea(int radius)
{
    // ...
}

public double CalculateArea(double radius)
{
    return Math.PI * radius * radius;
}
```
<br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}