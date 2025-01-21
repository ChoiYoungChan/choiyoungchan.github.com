---
title:  "[C#] C#에서 Dynamic Programming(다이내믹 프로그래밍) 사용법과 설명 완벽 정리 (C# 예시 코드 포함)"
excerpt: C# 에서 사용하는 Dynamic Programming

categories:
  - C Sharp
tags:
  - [C#, Dynamic Programming, 다이내믹 프로그래밍]

toc: true
toc_sticky: true
 
date: 2023-09-05
last_modified_at: 2023-09-05
---

## 개요
Dynamic Programming이란? <br>
=> DP(Dynamic Programming) 그러니까 동적 프로그래밍의 기본적인 개념은 매우 간단 합니다. <br>
하나의 큰 문제를 여러개의 작은 문제로 나누고, 작은 문제의 결과값을 저장했다가 다시 큰 문제를 해결할때 꺼내서 사용하는 방식 입니다. <br>


### 사용하는 이유
위의 부분에서 큰 문제를 작은문제 여러개로 나누어서 해결 한다는 부분에서 재귀를 떠올리시는 분이 많으실 겁니다. <br>
하지만 가장 큰 차이점은, 일반적인 재귀는 단순히 사용 시 동일한 작은 문제들이 여러 번 반복 되어 비효율적인 계산을 할 수 있다 라는점 입니다. <br><br>

재귀와의 차이점은 그렇다하고 왜 DP를 사용해야 되느냐, <br>
먼저 중복되는 계산을 피할 수 있습니다. DP를 사용하면 부분 문제의 결과를 저장하고 재사용할 수 있습니다. <br>
따라서 동일한 부분 문제를 반복적으로 계산하지 않아도 됩니다. <br>

중복되는 계산을 피함으로 인해 효율적인 문제 해결이 가능합니다. <br>
DP를 사용하면 문제를 작은 부분 문제로 나누어 해결합니다. 따라서 문제의 크기가 커져도 효율적으로 문제를 해결할 수 있습니다. <br>


### 사용조건
DP를 사용하기 위해서는 먼저 ```겹치는 부분``` 그리고 ```최적 부분의 구조``` 를 파악해야 합니다.<br>
기본적으로 문제를 여러개의 작은 문제로 소분 하고 그 문제의 결과값을 저장해 재활용하여 전체의 답을 구하는 구조인데, <br>
이는 ***동일한 작은 문제들이 반복적으로 나타나는 경우*** 사용 가능하다는 뜻 입니다. <br>

최적 부분의 구조는 부분 문제의 최적 결과값을 사용해 전체 문제의 최적의 결과를 낼 수 있는 경우를 의미 합니다. <br>
그래서 ***특정 문제의 정답은 문제 크기에 상관없이 동일*** 합니다. <br>


### Divide and Conquer(분할 정복)와 차이점

DP는 부분 문제를 해결한 결과를 메모리에 저장하여 재사용하는 방식입니다. 
그러니까.. 한 번 계산한 결과를 다시 계산하지 않고, 메모리에서 바로 가져와 사용합니다. 이로 인해 DP는 부분 문제를 반복적으로 해결해야 하는 경우에 효율적입니다.

Divide and Conquer는 부분 문제를 재귀적으로 나누어 해결하는 방식입니다.
즉, 문제를 가장 작은 부분으로 나눈 다음, 각 부분 문제를 해결하고, 그 결과를 합하여 전체 문제를 해결합니다. 이로 인해 Divide and Conquer는 부분 문제가 서로 독립적인 경우에 효율적입니다.


---
## 사용방법
---

1. DP로 풀 수 있는 문제인지 확인
2. 문제의 변수 파악
3. 변수 간 관계식 만들기(점화식)
4. 메모하기(memoization or tabulation)
5. 기저 상태 파악
6. 구현하기

<br>

Dynamic Programming은 ***특정한 경우에 사용하는 알고리즘이 아니라 하나의 방법*** 이므로 다양한 문제해결에 쓰일 수 있습니다.<br>
그래서 DP를 적용할 수 있는 문제 인지를 알아내는 부분부터 코드를 짜는 과정까지 난이도가 쉬운 것부터 어려운 것까지 매우 다양합니다.<br>

<br>
DP의 종류로는 아래의 2가지로 나눌 수 있습니다. <br>

1. Top to Bottom(재귀 사용)
2. Bottom to Top(반복문 사용)
<br> 


### 예제
--- 

피보나치 수열을 예시로 각각 Top to Bottom, Bottom to Top, 재귀로 해결하는 예시 코드 <br> 

[Bottom to Top 예제] <br> 
```c#
using System;
using System.Collections.Generic;

class FibonacciSampleCode
{
    public static int BottomtoTop(int number)
    {
        // 기저 상태
        int[] dp = new int[number + 1];
        dp[0] = 0;
        dp[1] = 1;

        // DP 테이블 채우기
        for (int count = 2; count <= number; count++) {
            dp[count] = dp[count - 1] + dp[count - 2];
        }

        // 결과 반환
        return dp[number];
    }

    public static void Main(string[] args)
    {
        // 입력
        int _number = 10;

        // 재귀 호출
        Console.WriteLine("BottomtoTop : " + BottomtoTop(_number));
    }
}
```
<br>

[Top to Bottom(재귀 사용) 예제] <br> 
```c#
using System;
using System.Collections.Generic;

class FibonacciSampleCode
{
    public static int Fibonacci(int number)
    {
        // 기저 상태
        if (number <= 1) return number;

        // 재귀 호출
        return Fibonacci(number - 1) + Fibonacci(number - 2);
    }

    public static void Main(string[] args)
    {
        // 입력
        int _number = 10;

        // 재귀 호출한 결과를 출력
        Console.WriteLine("재귀 : " + Fibonacci(_number));
    }
}
```
<br>

<br>
[Top](#){: .btn .btn--primary }{: .align-right}