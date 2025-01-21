---
title:  "[Algorithm] 이진 탐색(Binary Search)쉽게 배우기 (C++ 코드 예제 포함)"
excerpt: 이진 탐색(Binary Search)

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 이진 탐색, Binary Search]

toc: true
toc_sticky: true
 
date: 2023-04-05
last_modified_at: 2023-04-05
---

## 이진 탐색(Binary Search)란?
---
이진 탐색은 정렬된 배열이나 리스트에서 특정 값의 위치를 찾는 효율적인 알고리즘입니다. 탐색 범위를 절반씩 줄여나가기 때문에 선형 탐색(처음부터 끝까지 하나씩 확인하는 방식)보다 훨씬 빠릅니다.<br>
마치 책에서 원하는 페이지를 찾을 때, 책의 중간을 펼쳐보고 찾고자 하는 페이지보다 앞인지 뒤인지 확인하여 탐색 범위를 줄여나가는 것과 같습니다.
<br><br>

### 동작 방식
---
1. 탐색 범위를 전체 배열 또는 리스트로 설정합니다. (시작 인덱스 ```low```, 끝 인덱스 ```high```)
2. 탐색 범위의 중간 인덱스 ```mid```를 계산합니다. (```mid = (low + high) / 2```)
3. 중간 인덱스의 값 ```arr[mid]```과 찾고자 하는 값 ```target```을 비교합니다.
   * ```arr[mid] == target:``` 두 값이 같으면 탐색 성공! ```mid```를 반환합니다.
   * ```arr[mid] < target:``` 찾고자 하는 값이 중간 값보다 크면, 탐색 범위를 중간 인덱스의 오른쪽으로 좁힙니다. ```(low = mid + 1)```
   * ```arr[mid] > target:``` 찾고자 하는 값이 중간 값보다 작으면, 탐색 범위를 중간 인덱스의 왼쪽으로 좁힙니다. ```(high = mid - 1)```
4. ```low > high```가 될 때까지 2-3단계를 반복합니다. 이 조건이 되면 탐색 실패입니다.

<br><br>

### 장단점
---

#### 장점
* 뛰어난 효율성: 시간 복잡도는 O(log n)입니다. 즉, 데이터의 개수가 두 배로 늘어날 때 탐색 시간은 선형적으로 늘어나는 것이 아니라 로그 함수적으로 늘어납니다. 따라서 데이터가 많을수록 선형 탐색에 비해 압도적으로 빠릅니다.
* 간단한 구현: 알고리즘의 개념이 비교적 간단하여 코드로 구현하기 쉽습니다.

#### 단점
* 정렬된 데이터 필수: 이진 탐색을 사용하려면 데이터가 반드시 오름차순 또는 내림차순으로 정렬되어 있어야 합니다. 정렬되지 않은 데이터에는 사용할 수 없습니다. 정렬되지 않은 데이터에 이진 탐색을 적용하려면 먼저 정렬을 수행해야 합니다.

<br><br>


## 예제
---

[샘플 코드]
```C++
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};

    // std::binary_search 사용
    if (std::binary_search(numbers.begin(), numbers.end(), 23)) {
        std::cout << "23 found!" << std::endl;
    } else {
        std::cout << "23 not found." << std::endl;
    }

    if (std::binary_search(numbers.begin(), numbers.end(), 42)) {
        std::cout << "42 not found." << std::endl;
    }

    // std::lower_bound 사용
    auto lower15 = std::lower_bound(numbers.begin(), numbers.end(), 15);
    std::cout << "Lower bound of 15: " << *lower15 << " (index: " << std::distance(numbers.begin(), lower15) << ")" << std::endl; // 16 (index: 4)

    auto lower16 = std::lower_bound(numbers.begin(), numbers.end(), 16);
    std::cout << "Lower bound of 16: " << *lower16 << " (index: " << std::distance(numbers.begin(), lower16) << ")" << std::endl; // 16 (index: 4)

    // std::upper_bound 사용
    auto upper15 = std::upper_bound(numbers.begin(), numbers.end(), 15);
    std::cout << "Upper bound of 15: " << *upper15 << " (index: " << std::distance(numbers.begin(), upper15) << ")" << std::endl; // 16 (index: 4)

    auto upper16 = std::upper_bound(numbers.begin(), numbers.end(), 16);
    std::cout << "Upper bound of 16: " << *upper16 << " (index: " << std::distance(numbers.begin(), upper16) << ")" << std::endl; // 23 (index: 5)

    return 0;
}
```

<br><br>


[Top](#){: .btn .btn--primary }{: .align-right}