---
title:  "[C++] C++에서 사용하는 동기 비동기"
excerpt: synchronous and asynchronous in C++

categories:
  - Cpp
tags:
  - [C++, synchronous, asynchronous, 비동기, 동기]

toc: true
toc_sticky: true
 
date: 2023-01-28
last_modified_at: 2023-01-28
---

## 동기 비동기의 개념 
---
동기(synchronous) : 작업을 요청한 후 작업이 완료될 때까지 기다리는 방식입니다. 즉, 호출자는 피호출자의 작업이 끝날 때까지 블록(Block)됩니다. 마치 두 사람이 동시에 같은 일을 처리하는 것처럼, 한 사람이 작업을 마치기 전까지 다른 사람은 기다려야 합니다.<br><br>
비동기(asynchronous) : 작업을 요청한 후 작업이 완료되기를 기다리지 않고 다른 작업을 수행할 수 있는 방식입니다. 작업의 완료는 콜백 함수, 이벤트, 또는 Future/Promise와 같은 메커니즘을 통해 통지됩니다. 마치 여러 사람이 각자 다른 일을 처리하는 것처럼, 한 사람이 다른 사람의 작업이 끝날 때까지 기다릴 필요가 없습니다.

<br>

C#에서 동기 비동기 -> (https://choiyoungchan.github.io/c%20sharp/synchronous-asynchronous/)
<br><br>


### 동작 방식
---
#### 동기(synchronous)
1. 함수 또는 작업을 호출합니다.
2. 호출된 함수 또는 작업이 완료될 때까지 기다립니다.
3. 결과를 반환받습니다.
4. 다음 작업을 진행합니다.

#### 비동기(asynchronous)
1. 함수 또는 작업을 호출합니다.
2. 호출된 함수 또는 작업은 백그라운드에서 실행됩니다.
3. 호출자는 즉시 제어를 반환받아 다른 작업을 수행할 수 있습니다.
4. 작업이 완료되면 콜백 함수가 호출되거나 이벤트가 발생하거나, <br>
   Future/Promise를 통해 결과를 얻을 수 있습니다.

<br>

### 장단점
---
#### 장점

#### 동기(synchronous)
* 구현이 비교적 간단하고 직관적이라 코드의 흐름을 이해하기 쉽습니다.
* 작업의 완료 시점을 명확하게 알 수 있습니다.

#### 비동기(asynchronous)
* 프로그램의 응답성이 향상됩니다. 긴 작업을 수행하더라도 다른 작업을 계속 처리할 수 있습니다.
* 자원 활용률이 높아집니다. I/O 작업을 수행하는 동안 CPU는 다른 작업을 처리할 수 있습니다.

#### 단점

#### 동기(synchronous)
* 긴 작업을 수행하는 경우, 호출자는 작업이 완료될 때까지 기다려야 하므로 프로그램의 응답성이 떨어질 수 있습니다. 특히 GUI 환경에서는 사용자 인터페이스가 멈추는 현상이 발생할 수 있습니다.
* 자원 활용률이 낮아질 수 있습니다. 예를 들어, I/O 작업을 수행하는 동안 CPU는 아무 작업도 하지 않고 기다려야 합니다.

#### 비동기(asynchronous)
* 구현이 비교적 복잡합니다. 콜백 함수, 이벤트 처리, 또는 Future/Promise와 같은 추가적인 메커니즘이 필요합니다.
* 코드의 흐름을 추적하기 어려울 수 있습니다.

<br><br>

### 사용처
---

* 게임중 용량이 큰 파일(동영상 등등)을 로드할 때
* SDK나 기타 필요 라이브러리 등을 처음 로드할 때
* 순서가 확실하게 정해져 있는 작업을 할 때

<br>

### synchronous와 asynchronous 비교
---

![thread_00](https://github.com/user-attachments/assets/b84ceb6e-b6ae-4a01-b950-4f3d4a7d44a2)

<br><br>

### 예제
--- 

[동기(synchronous)]
```c++
#include <iostream>
#include <chrono>
#include <thread>

int long_operation(int x) {
    std::this_thread::sleep_for(std::chrono::seconds(2)); // 2초 동안 대기
    return x * 2;
}

int main() {
    std::cout << "Start" << std::endl;
    int result = long_operation(5); // 동기 호출: long_operation이 끝날 때까지 기다림
    std::cout << "Result: " << result << std::endl;
    std::cout << "End" << std::endl;
    return 0;
}
```
<br>

[비동기(asynchronous)]
```c++
#include <iostream>
#include <future>
#include <chrono>
#include <thread>

int long_operation(int x) {
    std::this_thread::sleep_for(std::chrono::seconds(2));
    return x * 2;
}

int main() {
    std::cout << "Start" << std::endl;
    std::future<int> result_future = std::async(std::launch::async, long_operation, 5); // 비동기 호출
    std::cout << "Doing other work..." << std::endl; // 다른 작업 수행
    int result = result_future.get(); // 결과 얻기 (필요한 시점에)
    std::cout << "Result: " << result << std::endl;
    std::cout << "End" << std::endl;
    return 0;
}
```

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}