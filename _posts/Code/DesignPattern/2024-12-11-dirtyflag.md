---
title:  "[Design Pattern] 더티플래그(DirtyFlag) 패턴"
excerpt: DirtyFlag Pattern

categories:
  - Design Pattern
tags:
  - [Design Pattern, DirtyFlag, DirtyFlag Pattern, 더티플래그 패턴, 디자인 패턴]

toc: true
toc_sticky: true
 
date: 2025-01-15
last_modified_at: 2025-01-15
---

## 더티플래그(DirtyFlag) 패턴이란?
---
더티 플래그 패턴은 불필요한 연산을 피하기 위해, 데이터가 변경되었는지 여부를 나타내는 플래그(flag)를 사용하여 필요한 경우에만 연산을 수행하는 최적화 기법입니다. <br>"더티(dirty)"라는 용어는 "오염되었다" 또는 "변경되었다"라는 의미로, 플래그가 "더티" 상태일 때 데이터가 변경되었음을 나타냅니다. 마치 빨래 바구니에 "세탁 필요" 깃발을 꽂아두는 것과 같습니다. 깃발이 꽂혀 있을 때만 세탁을 하고, 깨끗한 옷에는 불필요하게 세탁을 하지 않는 것처럼, 더티 플래그는 데이터가 변경되었을 때만 필요한 연산을 수행하여 성능을 향상시킵니다.

<br><br>

### 더티플래그(DirtyFlag) 패턴의 구성 요소
---
* 데이터: 연산의 대상이 되는 데이터입니다.
* 플래그 (Dirty Flag): 데이터의 변경 여부를 나타내는 불리언 변수입니다. 일반적으로 데이터가 변경되면 true (더티 상태), 변경되지 않았으면 false (클린 상태)로 설정됩니다.
* 연산: 데이터에 대해 수행되는 계산 또는 처리입니다.
<br><br>

### 더티플래그(DirtyFlag) 패턴의 작동 방식
---
1. 데이터가 변경될 때마다 해당 데이터와 관련된 플래그를 "더티" 상태 (true)로 설정합니다.
2. 데이터를 사용하는 코드에서, 데이터를 사용하기 전에 플래그를 확인합니다.
3. 플래그가 "더티" 상태이면, 필요한 연산을 수행하고 플래그를 "클린" 상태 (false)로 설정합니다.
4. 플래그가 "클린" 상태이면, 이전에 계산된 값을 그대로 사용하고 연산을 생략합니다.
<br><br>

### 더티플래그(DirtyFlag) 패턴의 장단점
---
#### 장점
* 불필요한 연산 방지: 데이터가 변경되지 않았을 때 불필요한 연산을 수행하지 않으므로, CPU 사용량을 줄이고 성능을 향상시킬 수 있습니다. 특히, 계산 비용이 높은 연산의 경우 효과가 큽니다.
* 캐싱 효과: 이전에 계산된 값을 저장해두고 재사용하므로, 캐싱과 유사한 효과를 얻을 수 있습니다.
* 간단한 구현: 비교적 간단하게 구현할 수 있으며, 코드의 가독성을 해치지 않으면서 최적화를 수행할 수 있습니다.

#### 단점
* 플래그 관리의 오버헤드: 플래그를 관리하는 추가적인 코드가 필요하며, 경우에 따라 미세한 성능 저하를 유발할 수 있습니다. 하지만, 대부분의 경우 연산 비용 절감 효과가 훨씬 크기 때문에 문제가 되지 않습니다.
* 동시성 문제 고려: 멀티 스레드 환경에서 데이터를 공유하는 경우, 동시성 문제를 고려하여 플래그를 안전하게 관리해야 합니다. 예를 들어, 뮤텍스(mutex) 또는 아토믹 변수(atomic variable)를 사용하여 플래그에 대한 접근을 동기화해야 합니다.
<br><br>


### 활용 예시
---
* 3D 그래픽스: 오브젝트의 변환 행렬(transformation matrix)을 계산할 때, 오브젝트의 위치, 회전, 크기가 변경되었을 때만 행렬을 다시 계산합니다.
* 게임 엔진: 게임 오브젝트의 물리 연산을 수행할 때, 오브젝트의 물리 속성이 변경되었을 때만 물리 시뮬레이션을 다시 수행합니다.
* UI 업데이트: UI 요소의 내용이 변경되었을 때만 UI를 다시 그립니다.
* 데이터베이스 동기화: 로컬 데이터베이스와 서버 데이터베이스를 동기화할 때, 변경된 데이터만 서버에 전송합니다.
<br><br>

## 예시코드
---

```C++
#include <iostream>

class Transform {
private:
    float x_, y_, z_; // 위치
    bool isDirty_;    // 더티 플래그
    float matrix_[4][4]; // 변환 행렬 (간략화)

public:
    Transform(float x, float y, float z) : x_(x), y_(y), z_(z), isDirty_(true) {}

    void SetPosition(float x, float y, float z) {
        x_ = x;
        y_ = y;
        z_ = z;
        isDirty_ = true; // 위치가 변경되었으므로 플래그를 더티 상태로 설정
    }

    float GetX() const { return x_; }
    float getY() const { return y_; }
    float getZ() const { return z_; }

    const float (*GetMatrix())[4] {
        if (isDirty_) {
            // 변환 행렬 계산 (실제로는 더 복잡한 계산이 필요)
            std::cout << "Calculating matrix..." << std::endl;
            matrix_[0][0] = 1; matrix_[0][1] = 0; matrix_[0][2] = 0; matrix_[0][3] = x_;
            matrix_[1][0] = 0; matrix_[1][1] = 1; matrix_[1][2] = 0; matrix_[1][3] = y_;
            matrix_[2][0] = 0; matrix_[2][1] = 0; matrix_[2][2] = 1; matrix_[2][3] = z_;
            matrix_[3][0] = 0; matrix_[3][1] = 0; matrix_[3][2] = 0; matrix_[3][3] = 1;
            isDirty_ = false; // 계산이 완료되었으므로 플래그를 클린 상태로 설정
        }
        return matrix_;
    }
};

int main() {
    Transform transform(1, 2, 3);

    // 처음 행렬을 가져올 때 계산이 수행됨
    const float (*matrix1)[4] = transform.GetMatrix();
    std::cout << transform.GetX() << std::endl;

    // 위치를 변경하지 않고 다시 행렬을 가져오면 계산이 생략됨
    const float (*matrix2)[4] = transform.GetMatrix();
    std::cout << transform.getY() << std::endl;


    transform.SetPosition(4, 5, 6); // 위치 변경

    // 위치가 변경되었으므로 다시 계산이 수행됨
    const float (*matrix3)[4] = transform.GetMatrix();
    std::cout << transform.getZ() << std::endl;

    return 0;
}
```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}