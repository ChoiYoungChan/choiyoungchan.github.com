---
title:  "[C++] Atoi함수 구현"
excerpt: 직접 c++에서 atoi함수를 구현해 보자

categories:
  - C++
tags:
  - [c++, Atoi]

toc: true
toc_sticky: true
 
date: 2022-08-08
last_modified_at: 2022-08-08
---

## Atoi의 개념
---
* 문자열을 정수로 변환한다.
* 문자열 초반의 공백은 무시한다.(아스키 코드로는 9~13, ''는 아스키 코드로 32)
* (+) 또는 (-) 부호는 최대 1개 까지만 올 수 있다.
* 숫자를 읽기 시작해서 다른 문자가 나오기 직전까지만 숫자를 읽는다.


## 코드 및 주석
---

<선언 및 main>
![atoi_00](https://user-images.githubusercontent.com/40765022/183655865-ae177f1d-dd17-4d88-9ee4-18c36e89b69b.png) <br>

<Atoi 함수 정의>
![atoi_01](https://user-images.githubusercontent.com/40765022/183655939-bb40f24f-20d1-48dd-96ff-63fc8eaf6ac7.png) <br>

<전체 코드>
![atoi_02](https://user-images.githubusercontent.com/40765022/183656298-ba1bae2d-2158-4412-a704-a934f85b8abc.png)<br>

## 실행 결과
---
### 부호를 붙이지 않으면
---
![atoi_02](https://user-images.githubusercontent.com/40765022/183655415-9292426b-85e0-4f5a-8a85-b8de01a3104e.png)

양수로 취급하여 출력 <br><br>

---

### - 부호 추가
---
![atoi_03](https://user-images.githubusercontent.com/40765022/183655481-86186eb4-456a-4023-b893-16bd89c724e0.png)


<br>

[Top](#){: .btn .btn--primary }{: .align-right}