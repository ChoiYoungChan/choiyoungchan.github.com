---
title:  "[C++] C++에서 3항연산자(ternary operator) 기본 개념 및 사용법 정리(C++ 코드 포함)"
excerpt: ternary operator

categories:
  - Cpp
tags:
  - [Programming, c++, ternary operator, Cpp]

toc: true
toc_sticky: true
 
date: 2022-08-12
last_modified_at: 2022-08-12
---

## 3항연산자의 개념
---
<br>

현직에서 if문이 길어지면 가독성이 떨어지고 불편할 때가 있습니다. <br>
그때 if문을 간단해 대체할 수 있는것이 삼항연산자이며, <br> 
이 삼항연산자는 유일하게 피연산자를 3개나 가지는 조건 연산자 입니다. 
<br>

[기본 문법]

```
조건 ? 참일경우 실행 : 거짓일 경우 실행 ;
```
* ? 앞의 조건식에 따라 결과 값이 참(true)이면 : 앞의 것을, 거짓(false)일 경우 : 뒤의 것을 실행합니다.

<br>

## 코드 및 주석
---

[기본]
아래와 같이 기본적인 문법은 매우 간단합니다.

```c++
int main()
{
	int a = 10, b = 15;

	(a < b) ? printf("a가 더 크다") : printf("b가 더 크다");

}
```
? 앞에 있는 조건식 이 참(true)일경우 ``` printf("a가 더 크다")``` 가 실행되며, <br>
거짓(false)일 경우 ``` printf("b가 더 크다")``` 가 실행 됩니다.

 <br>

[응용]
1. 실행할 내용이 변수에 값을 넣어줄 때(변수 1개)

```c++
int main()
{
	int a = 10, b = 15, c = 0, d = 0;
	c = (a > b) ? 1 : 0;

	printf("c = %d, d = %d", c, d);
}
```
 <br>

2. 실행할 내용이 서로 다른 변수에 값을 넣어줄 때
```c++
int main()
{
	int a = 10, b = 15, c = 0, d = 0;
	(a < b) ? (c = 5) : (d = 6);

	printf("c = %d, d = %d", c, d);
}
```
 <br>

3. 실행할 내용이 변수에 값을 넣어줄 때(변수 여러개)
```c++
int main()
{
	int a = 10, b = 15, c = 0, d = 0;
	(a > b) ? (c = 38) : (c = 75, d = 20);
  
	printf("c = %d, d = %d", c, d);
}
```

 <br>

4. 기타 등등
```c++
int main()
{
	int a = 10, b = 15, c = 0, d = 0;

	(a < b) ? (printf("3항연산자 \n"), c = a, d = 72) : (c = 13);

	printf("c = %d, d = %d", c, d);
}
```

<br>



[Top](#){: .btn .btn--primary }{: .align-right}