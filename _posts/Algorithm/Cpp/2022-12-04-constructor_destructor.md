---
title:  "[C++] 생성자와 소멸자"
excerpt: Constructor Destructor

categories:
  - Cpp
tags:
  - [Cpp, C++, Constructor, Destructor, 생성자, 소멸자]

toc: true
toc_sticky: true
 
date: 2022-08-13
last_modified_at: 2022-08-13
---

## 생성자와 소멸자란?
---

### 생성자
객체가 생성될 때 자동으로 호출되는 멤버 함수로, 일반적으로 클래스내 멤버 변수의 초기화 또는 필요한 설정을 할 경우 사용됩니다. <br> 

생성자 규칙
1. 생성자 이름은 클래스와 이름이 같아야 한다.
2. 생성자는 리턴 타입이 없다. (void도 아니다)

<br>

### 소멸자
소멸자는 객체가 소멸될 때 자동으로 실행되는 클래스의 멤버 함수입니다. <br>
생성자는 클래스의 초기화를 돕도록 설계됐지만 소멸자는 청소를 돕도록 설계되었습니다. <br>
아래와 같은 규칙 때문에 소멸자는 클래스당 1개만 존재할 수 있으며, 소멸되기 전에 마지막으로 호출 되는 함수이므로 완벽하게 청소가 됩니다.<br>

1. 소멸자 이름은 클래스 이름과 같아야 하고 앞에 ~를 달아야 한다.
2. 소멸자는 인수가 없다.
3. 소멸자는 반환 값이 없다.


## 예제
---

### 생성자
---

생성자를 이용하는 방법은 크게 3가지가 있으며 그 방법은 아래와 같으며, 실무에서 기본적으로 사용하는 기초적이면서도 중요한 부분이기 때문에 <br>
전부 다 예제를 들어 살펴 보도록 하겠습니다.<br>

1. 기본 생성자
2. 매개변수가 있는 생성자
3. 매개변수가 있지만 기본처럼 사용할 수 있는 생성자

#### 기본 생성자
---

```C++
class TestCpp
{
public:
	TestCpp(); // 생성자
	void ShowInfo();

public:
	std::string m_name;
	int m_age;

};

/// <summary>
/// 생성자
/// </summary>
TestCpp::TestCpp()
{
	m_name = "TestCpp";
	m_age = 25;
}
```

#### 매개변수가 있는 생성자
---

아래의 예제에는 한 클래스 안에 2개의 생성자가 있습니다.
* 일반적인 경우 호출될 기본 생성자
* 2개의 매개 변수를 사용하는 생성자
 

이 2개의 생성자는 함수 오버로드로 인해 같은 클래스 안에서 공존할 수 있습니다.<br> 
실제로 각각 고유한 서명이므로 원하는 수 만큼 생성자를 정의할 수 있습니다.<br>

```C++
#pragma once
#include <iostream>

class TestCpp
{
public:
	TestCpp(); // 생성자
	TestCpp(std::string _name, int _age);

	void ShowInfo();
public:
	std::string m_name;
	int m_age;

};

/// <summary>
/// 생성자
/// </summary>
TestCpp::TestCpp()
{
	m_name = "TestCpp";
	m_age = 25;
}

TestCpp::TestCpp(std::string _name, int _age)
{
	m_name = _name;
	m_age = _age;
}
```
<br>

이 생성자를 매개 변수와 함께 사용하는 방법은 아래와 같이 직접 초기화 형식의 초기화를 사용하면 됩니다. <br>

```C++
#include "TestCpp.h"

int main()
{
	TestCpp _testCpp("name", 22);
	_testCpp.ShowInfo();
}
```

<br>


#### 매개변수가 있지만 기본처럼 사용할 수 있는 생성자
---
상기의 2가지 예제의 생성자를 아래와 같이 단순화 하는것도 가능합니다. <br>

```C++
#pragma once
#include <iostream>

class TestCpp
{
public:
	TestCpp(std::string _name, int _age);
	~TestCpp(); // 소멸자

	void ShowInfo();
public:
	std::string m_name;
	int m_age;

};

/// <summary>
/// 생성자
/// </summary>
/// <param name="_name"></param>
/// <param name="_age"></param>
TestCpp::TestCpp(std::string _name = "TestCpp", int _age = 22)
{
	m_name = _name;
	m_age = _age;
}

/// <summary>
/// 소멸자
/// </summary>
TestCpp::~TestCpp()
{
	m_name = "NULL";
	m_age = NULL;
	std::cout << "소멸자 호출, " << m_name << " : " << m_age << std::endl;
}

void TestCpp::ShowInfo()
{
	std::cout << m_name << " : " << m_age << std::endl;
}
```
<br>

main함수에서 호출 <br>

```C++
#include "TestCpp.h"

int main()
{
	TestCpp _testCpp; // m_name = TestCpp, m_age = 22
	TestCpp _testCpp("Constructor"); // m_name = Constructor, m_age = 22
	TestCpp _testCpp("Constructor", 23); // m_name = Constructor, m_age = 23

	_testCpp.ShowInfo();
}
```
<br>

### 소멸자

```C++
#pragma once
#include <iostream>

class TestCpp
{
public:
	TestCpp(); // 생성자
	~TestCpp(); // 소멸자

	void ShowInfo();
public:
	std::string m_name;
	int m_age;

};

/// <summary>
/// 생성자
/// </summary>
TestCpp::TestCpp()
{
	m_name = "TestCpp";
	m_age = 2;
}

/// <summary>
/// 소멸자
/// </summary>
TestCpp::~TestCpp()
{
	m_name = "NULL";
	m_age = NULL;
	std::cout << "소멸자 호출, " << m_name << " : " << m_age << std::endl;
}
```
<br>

실행 결과

```C++
소멸자 호출, NULL : 0
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}