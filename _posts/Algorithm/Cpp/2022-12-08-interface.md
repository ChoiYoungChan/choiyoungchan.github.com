---
title:  "[C++] Interface란"
excerpt: C++ 에서 사용하는 Interface란

categories:
  - Cpp
tags:
  - [Cpp, C++, Interface, 인터페이스]

toc: true
toc_sticky: true
 
date: 2022-12-08
last_modified_at: 2022-12-08
---

## 개요
Interface란?<br>
=> 한마디로 인터페이스는 Method 원형들의 집합에 이름을 붙인 것으로, 상속 받을 클래스에 기능이나 속성을 지정하는 역할을 합니다. <br>
C#이나 Java같은 다른 OOP언어에서는 인터페이스 형식을 제공하지만, C++에서는 인터페이스 형식을 제공하지 않고 순수 가상 Method를 이용하여 정의할 수 있습니다. <br>

C#에서 인터페이스 -> [C#]()  <br><br>


### 예제
--- 

InterFace
```c++
#pragma once
__interface ITest
{
	virtual void ShowText();
};
```
<br> 

Main Class.h
```c++
#pragma once
#include <iostream>
#include "ITest.h"

class TestCpp : public ITest
{
public:
	void ShowText() { std::cout << "Test Interface in C++" << std::endl; };
};

class MainTest
{
public:
	void ShowInfo(ITest* _test) { _test->ShowText(); };
private:

};
```
<br>

Main Class.cpp
```c++
#include "TestCpp.h"
int main()
{
	MainTest _mainTest;
	TestCpp _testCpp;

	_mainTest.ShowInfo(&_testCpp);
}
```

<br> 

전체 소스코드

```c++
#pragma once
#include <iostream>
#include "ITest.h"

class TestCpp : public ITest
{
public:
	void ShowText() { std::cout << "Test Interface in C++" << std::endl; };
};

class MainTest
{
public:
	void ShowInfo(ITest* _test) { _test->ShowText(); };
private:

};

int main()
{
	MainTest _mainTest;
	TestCpp _testCpp;

	_mainTest.ShowInfo(&_testCpp);
}
```


### build result

```
Test Interface in C++
```

<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}