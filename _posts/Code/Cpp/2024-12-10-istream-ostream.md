---
title:  "[C++] istream/ostream으로 입력 및 출력하는 방법(C++샘플 코드 첨부)"
excerpt: Perfect Forwarding and std::forward

categories:
  - Cpp
tags:
  - [C++, Cpp, std::forward, Perfect Forwarding, 완벽한 전달, forward]

toc: true
toc_sticky: true
 
date: 2024-12-10
last_modified_at: 2024-12-10
---

## 개요
---
C++에서는 표준 입출력을 위해 istream과 ostream을 제공합니다. istream은 입력 스트림을 처리하며, ostream은 출력 스트림을 처리합니다. 일반적으로 cin과 cout이 각각 istream과 ostream의 대표적인 객체입니다. 또한, 파일 입출력에서도 ifstream과 ofstream을 사용하여 파일을 읽고 쓸 수 있습니다.<br>
이 두 클래스를 통해 다양한 형태의 데이터를 효율적으로 처리할 수 있으니 익혀두시는것을 추천합니다.
<br><br>

### istream: 입력 스트림의 마법사
---
istream은 입력을 처리하는 스트림 클래스이며, 주로 키보드 입력이나 파일 입력을 다룰 때 사용됩니다. >> 연산자를 이용해 데이터를 읽어오며, 입력이 버퍼에서 제공됩니다.
<br><br>

#### 특징
---
* ```>>```연산자로 여러 개의 데이터를 연속해서 읽을 수 있음
* 공백(공백, 개행, 탭)을 기준으로 데이터를 구분함
* ```getline()```을 사용하면 한 줄 전체를 읽을 수 있음
* ```eof()```, ```fail()```, ```bad()```등의 함수를 사용하여 입력 상태를 확인할 수 있음

### istream 샘플 코드
---
```C++
#include <iostream>
#include <string>

int main() {
    int number;
    std::string text;
    
    std::cout << "숫자를 입력하세요: ";
    std::cin >> number; // 숫자 입력
    std::cin.ignore(); // 버퍼 비우기
    
    std::cout << "문장을 입력하세요: ";
    std::getline(std::cin, text); // 한 줄 입력
    
    std::cout << "입력된 숫자: " << number << "\n";
    std::cout << "입력된 문장: " << text << "\n";
    
    return 0;
}
```
<br>

### ostream: 출력 스트림의 마법사
---
ostream은 출력을 처리하는 스트림 클래스이며, 주로 콘솔이나 파일로 데이터를 출력할 때 사용됩니다. ```<<```연산자를 이용해 데이터를 출력하며, 출력 스트림 버퍼를 통해 데이터를 전달합니다.
<br><br>

#### 특징
---
* ```<<```연산자로 여러 개의 데이터를 연속해서 출력 가능
* std::endl 또는 \n을 사용하여 줄바꿈 가능
* flush()를 사용하여 출력 버퍼를 강제로 비울 수 있음
* 형식 지정자를 사용하여 출력 형식 조정 가능 (std::hex, std::fixed 등)

### ostream 샘플 코드
---
```C++
#include <iostream>

int main() {
    int a = 10;
    double b = 3.14159;
    
    std::cout << "정수: " << a << "\n";
    std::cout << "실수: " << b << "\n";
    std::cout << "16진수: " << std::hex << a << "\n";
    
    return 0;
}
```
<br>

## 주의사항
---
```cin```을 사용할 때 ```getline()```과 함께 사용하면 ```cin```버퍼 문제를 방지하기 위해 ```cin.ignore()```를 호출하는 것이 좋음.

입력이 실패하면 ```cin.clear()```와 ```cin.ignore()```를 사용하여 오류 상태를 정리할 필요가 있음.

```endl```을 사용하면 자동으로 버퍼가 비워지므로 불필요한 ```endl```사용을 줄이는 것이 성능에 좋음 ("\n"을 선호).
<br>

### 업무에서 사용하는 파일 입출력 예제
---
```C++
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ofstream outfile("output.txt"); // 파일 출력 스트림 생성
    if (!outfile) {
        std::cerr << "파일을 열 수 없습니다." << std::endl;
        return 1;
    }
    outfile << "Hello, File!" << std::endl;
    outfile.close();
    
    std::ifstream infile("output.txt"); // 파일 입력 스트림 생성
    if (!infile) {
        std::cerr << "파일을 열 수 없습니다." << std::endl;
        return 1;
    }
    std::string content;
    std::getline(infile, content);
    std::cout << "파일 내용: " << content << "\n";
    infile.close();
    
    return 0;
}
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}