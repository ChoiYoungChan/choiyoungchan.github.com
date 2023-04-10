---
title:  "[C++] 스마트 포인터"
excerpt: 스마트 포인터란

categories:
  - Cpp
tags:
  - [Cpp, C++, 스마트 포인터, smart pointer, pointer]

toc: true
toc_sticky: true
 
date: 2022-12-13
last_modified_at: 2022-12-13
---

## 스마트 포인터란?
---
간단히 말하면 포인터 처럼 사용하는 클래스 템플릿으로 메모리를 자동으로 해제해주는 기능이 스마트 포인터 입니다.<br>
다른 매니지드 언어의 경우 garbage collector등을 통해 메모리를 관리 하지만 c++는 언매니지드 언어 즉, 사용자가 스스로 메모리를 할당 해제를 통해 관리를 해야만 합니다.<br>
할당받은 메모리를  해제하지 않을 경우 프로그램은 계속 사용하고 있는 메모리라고 인지하여 해당 메모리를 사용하지 않는 메모리 누수가 발생합니다. <br>이를 방지 하기 위해 스마트 포인터를 이용하여 메모리를 자동으로 해제해 메모리 누수를 방지합니다.<br>

종류로는 아래의 3가지가 있습니다.
* shared_ptr
* unique_ptr
* weaked_ptr

### shared_ptr
---
shared_ptr은 어떤 하나의 객체를 참조하는 스마트 포인터의 개수를 참조하는 스마트 포인터입니다. <br>
이렇게 참조하고 있는 스마트 포인터의 개수를 reference count라고 하는데, 해당 메모리를 참조하는 포인터가 몇개인지 나타내는 값으로 shared_ptr가 추가될때 1씩 증가하고 수명이 다하면 1씩 감소하는 방식입니다. <br>

따라서 마지막 shared_ptr의 수명이 다하거나 main()함수가 종료되면 참조 카운트가 0이되어 delete를 사용하여 메모리를 자동으로 해제합니다. <br>

아래와 같이 make_shared() 함수를 이용하여 인스턴스 생성을 할 수 있습니다.  <br>

여기서, make_shared() 함수는 전달받은 인수를 사용하여 지정된 객체를 생성하고 생성된 객체를 참조하는 shared_ptr을 반환하기 때문에 해당 함수를 사용하면 shared_ptr 객체를 예외발생에 대해 안전하게 생성할 수 있습니다. <br>

```c++
shared_ptr<객체> 스마트 포인터명(new 객체);
shared_ptr<객체> 스마트 포인터명 = make_shared<객체>(인수);
```
<br>

### unique_ptr
---
unique_ptr은 shared_ptr와 달리 하나의 스마트 포인터만이 객체를 가리킬수 있도록 합니다. <br>
즉 reference count가 1을 넘길수 없으며, make_shared()함수 처럼 make_unique()함수를 사용하여 안전하게 인스턴스를 생성할 수 있습니다. <br>

```c++
unique_ptr<객체> 스마트 포인터명(new 객체)
unique_ptr<객체> 스마트 포인터명 = make_unique<객체>(인수);
```
<br>

### weaked_ptr
---
weak_ptr은 하나 이상의 shared_ptr가 가리키는 객체를 참조할수 있지만 reference count를 늘리지않는 스마트 포인터입니다. <br>
shared_ptr을 사용할때 발생할 수 있는 문제를 해결하기 위해 사용됩니다. <br>

shared_ptr은 하나의 객체를 여러 스마트 포인터가 가리키고 reference count를 통해 동작하는데 만약 서로가 서로를 가리키는 shared_ptr을 가지게 되면 reference count가 0이 될 수가 없어 메모리가 해제되지 않는 순환 참조(circular reference)가 발생하게 됩니다. <br>
weak_ptr은 이러한 순환 참조를 제거하기 위해 사용됩니다. <br>

```c++
shared_ptr<객체> lockedPtr = weak_f.lock();
```
<br>

## 예제
---

### shared_ptr
---

```c++
#include <iostream>
#include <memory> 

int main()
{
    // int형
    std::shared_ptr<int> shared_test_01(new int(15));
    std::shared_ptr<int> shared_test_02 = std::make_shared<int>(13);

    // string형 
    std::shared_ptr<std::string> shared_test_string_01(new std::string("shareded_ptr"));
    std::shared_ptr<std::string> shared_test_string_02 = std::make_shared<std::string>("Test");

    std::cout << *shared_test_01 << " : " << *shared_test_02 << std::endl;
    std::cout << *shared_test_string_01 << " : " << *shared_test_string_02 << std::endl;

    return 0;
}
```
<br>

### unique_ptr
---

```c++
#include <iostream>
#include <memory>

class TestCpp {
    int* data;

public:
    // Constructor
    TestCpp()
    {
        std::cout << "생성" << std::endl;
        data = new int[100];
    }

    void some() 
    {
        std::cout << "일반 포인터와 동일하게 사용" << std::endl;
    }

    // Destructor
    ~TestCpp() 
    {
        std::cout << "해제" << std::endl;
        delete[] data;
    }
};

void TestPtr()
{
    std::unique_ptr<TestCpp> _uniquePtr(new TestCpp());
    _uniquePtr->some();
}

int main()
{
    TestPtr();
}
```
<br>

### weaked_ptr
---

weaked_ptr는 상기의 unique_ptr, shared_ptr처럼 직접 원시 포인터에 접근 하는 방식이 아닙니다. <br>
그 이유는 weaked_ptr가 직접 원시 포인터 사이클에 관여를 해버리면 해당 원시 포인터를 참조하는 share_ptr인 존재하지 않아도 여전히 사용할 수 있기 때문입니다. <br>
그래서 내부의 멤버 함수 lock()을 이용하여 안전하고 간접적인 방법을 사용합니다. <br>

```c++
#include <iostream>
#include <memory> 

int main()
{
    std::shared_ptr<std::string> sharedptr_test(new std::string("weak_ptr Test")); // reference count = 1
    std::weak_ptr<std::string> weakptr_test = sharedptr_test; // reference count = 1

    std::cout << "shared_ptr : " << *sharedptr_test << " is in shared" << std::endl;
    
    {
        auto temp = weakptr_test.lock(); // reference count = 2
        std::cout << "weak_ptr : " << *temp << std::endl;
    } // 이 closure를 벗어나면서 temp는 해제된다. reference count = 1

    sharedptr_test.reset(); // reference count = 0

    return 0;
}
```
<br>


<br>

[Top](#){: .btn .btn--primary }{: .align-right}