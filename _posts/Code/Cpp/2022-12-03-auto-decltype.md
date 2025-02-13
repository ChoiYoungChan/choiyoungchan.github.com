---
title:  "[C++] 자료형 추론 auto, decltype에 대하여(C++ 샘플 포함)"
excerpt: auto & decltype

categories:
  - Cpp
tags:
  - [C++, Cpp, decltype, auto, 자료형 추론]

toc: true
toc_sticky: true
 
date: 2022-12-03
last_modified_at: 2022-12-03
---

## 개요
---
C++은 강력한 타입 시스템을 제공하지만, 때로는 타입을 명시적으로 작성하는 것이 번거롭거나 불필요한 경우가 있습니다. 이때 auto와 decltype은 타입 추론을 통해 코드의 간결성과 유연성을 높여주는 유용한 도구입니다. 마치 **"타입 추론 마법사"** 처럼, auto와 decltype은 컴파일러가 자동으로 변수의 타입을 추론하도록 도와줍니다.
<br><br>

### Auto
---
```auto```키워드는 변수를 선언할 때 초기값을 통해 변수의 타입을 자동으로 추론합니다. 마치 **"자동 타입 할당"** 처럼, ```auto```는 변수의 타입을 명시적으로 작성하지 않아도 컴파일러가 알아서 타입을 결정해줍니다.
<br><br>

### 예시 코드
---

1. auto &&
```c++
void ex()
{
	int number = 40;
	auto && rnum = number;	// rnum_는 l-value. int& rnum_ 왜냐하면 들어온게 l-value니까
	auto && rnum2 = 42;	    // rnum2는 r-value. int&& rnum2
	auto && rnum3 = std::move(number); // rnum3는 r-value.  int && rnum3
}
```
<br>

2. auto 는 긴 타입을 간결하게 줄여줍니다.
```c++
using namespace std;

void example()
{
	vector<int> vect;

	for (vector<int>::const_iterator cit = vect.begin(); cit != vect.end(); ++cit)
		cout << *cit;

	for (auto itr = vect.begin(); itr != vect.end(); ++itr)
		cout << *itr;

	for (auto itr : vect)
		cout << itr;
}
```
<br>

3. auto 는 const &, volatile 같은 추가 지정은 읽지 않는다.
```c++
void example()
{
	int integer = int();		// integer is an int, initialized to 0
	auto auto_integer = integer;

	const int& crx = integer; // crx is a const int& that refers to integer. 다른 건 못 참조하고 고정.
	auto auto_crx1 = crs;
	const auto& auto_crx2 = crx;

	volatile int vx = 1024;
	auto avx = vx;
	volatile auto vavx = vx;
}
```
<br>

4. auto & 경우에는 const를 읽는다.
```c++
void example()
{
	const int integer = 0;
	auto& autovar = integer;
    // autovar = 123 - error!
}
```
<br>

5. auto 포인터일 경우에는 const, *를 다 읽어들인다
```c++
void example()
{
	int integer = 40;
	const int* pi = &integer;
	auto autovar = pi;		
    
  // 이번에는 int가 아니라 const int * 까지 다 가져옴
	// 즉, 포인터일 경우에는 auto가 값을 다 가져오는 것을 알 수 있음
}
```
<br>

6. auto 람다 함수는 파라미터에 auto를 사용할 수 있다.
```c++
void example()
{
	// generic lambda;
	auto func = [](auto x, auto y) {return x + y; };
	cout << func(1.1, 5) << "  " << func(3.7, 23.1) << '\n';
	// 람다 함수는 parameter로 auto를 사용 가능
}
```
<br><br>

### decltype
---
```decltype```키워드는 표현식의 타입을 그대로 추론합니다. 마치 **"타입 복사"** 처럼, ```decltype```은 표현식의 타입을 정확하게 가져와 변수의 타입을 결정합니다.
<br><br>

### 예시 코드
---
1. decltype은 리턴 타입에도 사용 가능 하다.
```c++
template<typename T1, typename T2>
auto example_func(T1 lvar, T2 rvar) -> decltype(lvar* rvar)
{	
	return lvar * rvar;
}
```
<br>

2. decltype(( ))
```c++
struct Struct
{
	int mat_xPos;  // m_x 멤버를 가지고 있고
	Struct()
	{
		mat_xPos = 42;  // 구조체를 생성하면 m_x 값을 42 로 초기화 한다.
	}
};
```
```c++
void example()
{
	int integer;
	const int cx = 42;
	const int& crx = integer;   // crx는 integer를 참조하며 const로서 참조하는 대상을 integer에서 다른걸로 바꿀 수 없다.
	const Struct* pointer = new Struct();  // 구조체 Struct의 포인터 pointer는 const로서 가리키는 대상을 new Struct()에서 다른걸로 바꿀 수 없다.

	auto auto1 = integer;     // int
	auto auto2 = cx;		      // int   (const int 가 아님)
	auto auto3 = crx;		      // int   (const int & 가 아님)
	auto auto4 = p;	          // const Struct *  (포인터라 그대로 다 따라 온다.)
	auto auto5 = p->m_x;      // int  (p는 const 포인터이기 때문에 간접참조로 구조체 멤버의 값을 바꿀 수 없고 p->mat_xPos 이렇게 읽을 수만 있다.)

	typedef decltype(integer) x_type;		    // int
	typedef decltype(cx) cx_type;		        // const int
	typedef decltype(crx) crx_type;		      // const int &	
	typedef decltype(p->m_x) m_x_type;	    // int
									
	typedef decltype((integer)) cx_type;				      // int &
	typedef decltype((cx)) cx_with_parens_type;		    // const int &
	typedef decltype((crx)) crx_with_parens_type;	    // const int &  (원래 레퍼런스였다면 그대로 & 유지함)	
	typedef decltype((p->m_x)) m_x_with_parens_type;	// const int & 	  (p는 const이기 때문에 간접참조로 멤버의 값을 바꾸면 안되기 때문에 & 레퍼런스가 되니 값을 바꾸면 안된다는 const까지 따라왔다.)
}
```
<br>

3. 리턴 타입을 auto 와 decltype 에 넣을 때.
```c++
const Struct foo() { return Struct(); }             // const 구조체 Struct() 를 리턴한다.
const int& foobar() { return 123; }                 // const int & 를 리턴한다.

void example()
{
	vector<int> vec = { 10, 20 };

	auto auto1 = foo();									    // Struct        
	typedef decltype(foo()) foo_type;				// const Struct

	auto auto2 = foobar();								  // int
	typedef decltype(foobar()) foobar_type;	// const int &

	auto itr = vec.begin();							    // std::vector<int>::iterator
	typedef decltype(vec.begin()) iterator_type;	// std::vector<int>::iterator

	auto firstElement = vec[0];						  // int
	decltype(vec[0]) secondElement = vec[0];	    // int &
}
```
<br>

4. L-value, R-value
```c++
void example()
{
	int xPos = 0;
	int yPos = 0;
	const int cx = 40;
	const int cy = 50;
	double d1 = 3.14;
	double d2 = 9.8;

	typedef decltype(xPos * yPos) prod_xy_type;		// int
	auto auto1 = xPos * yPos;										  // int
		
	typedef decltype(cx * cy) prod_cxcy_type;			// int
	auto auto2 = cx * cy;									        // int

	typedef decltype(d1 < d2 ? d1 : d2) cond_type;// double &
	auto auto3 = d1 < d2 ? d1 : d2;							  // double

	typedef decltype(xPos < d2 ? xPos : d2) cond_type_mixed;	// double
	auto auto4 = xPos < d2 ? xPos : d2;						// double
}
```
<br>

5. decltype 레퍼런스 없애기 std::remove_reference
```c++
template<typename T1, typename T2>	// decltype 특성상 두 인수 T1과 T2의 자료형이 같을 경우 &가 붙는다는 단점이 존재한다.
auto fpmin_wrong(T1 xPos, T2 yPos) -> decltype(xPos < yPos ? xPos : yPos) 
{ 
	return xPos < yPos ? xPos : yPos; 
}

template<typename T1, typename T2>	// 두 인수가 자료형이 같을 경우 &가 붙는 단점을 없애버린다.
auto fpmin(T1 xPos, T2 yPos) -> typename std::remove_reference<decltype(xPos < yPos ? xPos : yPos)>::type
{ 
	return xPos < yPos ? xPos : yPos; 
}

void example()
{
	int integer = 42;
	double doublenum = 45.1;
	auto autovar = std::min(static_cast<double>(integer), doublenum);

	int &secondnum = integer;

	typedef decltype(fpmin_wrong(doublenum, doublenum)) fpmin_return_type1;  // double &
	typedef decltype(fpmin_wrong(integer, doublenum)) fpmin_return_type2;    // double
	typedef decltype(fpmin_wrong(secondnum, doublenum)) fpmin_return_type3;  // double
  typedef decltype(fpmin(doublenum, doublenum)) fpmin_return_type4;        // double
}
```
<br>

6. decltype 은 런타임이 아닌 컴파일 타임에 결정 된다.
```c++
void example()
{
	vector<int> vect;
	typedef decltype(vect[0]) integer;	// decltype 에서는 '런타임 실행'하지는 않으므로 문제 X
}
```
<br><br>

###  auto와 decltype의 차이점
---
![Image](https://github.com/user-attachments/assets/187ac3a9-25d2-4185-ab7a-67fc4a320339)

<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}