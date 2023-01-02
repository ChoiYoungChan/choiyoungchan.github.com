---
title:  "[C++] C++에서 사용하는 중첩 클래스"
excerpt: Nested class in C++

categories:
  - Cpp
tags:
  - [C++, Nested class, 중첩 클래스]

toc: true
toc_sticky: true
 
date: 2022-12-22
last_modified_at: 2022-12-22
---

## 개요
중첩 클래스란?<br>
=> 클래스를 다른 클래스의 범위 내에서 선언할 수있으며, 이러한 방식을 "중첩 클래스"라고 합니다. <br>
중첩 클래스는 바깥쪽 클래스의 범위 내에 있는 것으로 간주되며 해당 범위 내에서 사용할 수 있습니다.  <br>
바로 바깥쪽 범위 이외의 범위에서 중첩 클래스를 참조하려면 정규화된 이름을 사용해야 합니다. <br>

중첩 클래스를 사용하는 이유
* 클래스를 논리적으로 그룹화할 수 있습니다.
* 특정 클래스 내부에서만 사용되기 때문에 코드를 더 쉽게 파악할 수 있으며, 유지 관리가 쉽습니다.
* 특정 클래스 내부에서만 사용되므로 클래스 구조가 단순해집니다. (public으로 선언시 외부에서 접근 가능)

C#에서의 중첩 클래스또한 기본적인 개념은 비슷합니다. <br>
참조 -> [C++ Inner Class](https://choiyoungchan.github.io/c%20sharp/nested-class/) <br>

<br>

### 예제
--- 

TestCpp.h
```c++
#include <iostream>

class TestCpp
{
public:

	class TestInnerClass
	{
	public :
		void ShowText() { std::cout << "Inner Class test" << std::endl; }
	};

	TestInnerClass m_test_inner_class;

	void ShowTextData()
	{
		m_test_inner_class.ShowText();
	}
};
```
<br>

TestCpp.cpp
```c++
#include "TestCpp.h"

int main()
{
    TestCpp m_test_cpp;
    TestInnerClass m_test_inner_class; // 컴파일 에러
    m_test_cpp.ShowTextData();

    return 0;
}
```
<br>

상기에서는 ```TestCpp```내에서만 사용할 수 있도록 ```TestInnerClass```를 선언하고 main에서 TestCpp클래스르 만들어주는 예제입니다. <br>
외부에서 TestInnerClass클래스를 만들려고 하면 컴파일 에러가 발생합니다. <br>
하지만 Inner Class의 접근지정자가 public 일 경우 외부 클래스를 통해 접근을 할 수 있습니다. <br>
때문에, 아래의 ```TestCpp::TestInnerClass```형식으로 TestInnerClass 클래스를 만들어 사용할 수도 있습니다. <br>

```c++
#include "TestCpp.h"

int main()
{
    TestCpp::TestInnerClass m_test_inner_class;
    m_test_inner_class.ShowText();

    return 0;
}
```


<br> 
전체 소스코드

```c++
public:

	class TestInnerClass
	{
	public :
		void ShowText() { std::cout << "Inner Class test" << std::endl; }
	};

	TestInnerClass m_test_inner_class;

	void ShowTextData()
	{
		m_test_inner_class.ShowText();
	}
};

int main()
{
    TestCpp m_test_cpp;
    m_test_cpp.ShowTextData();

    return 0;
}
```

### build result

```
Inner Class test
```

<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}