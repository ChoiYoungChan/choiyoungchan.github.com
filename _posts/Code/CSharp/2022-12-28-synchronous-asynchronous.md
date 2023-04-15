---
title:  "[C#] C#에서 사용하는 동기 비동기"
excerpt: synchronous and asynchronous in C#

categories:
  - C Sharp
tags:
  - [C#, synchronous, asynchronous, 비동기, 동기]

toc: true
toc_sticky: true
 
date: 2022-12-28
last_modified_at: 2022-12-28
---

## 동기 비동기의 개념 및 사용처

동기 <br>
일반적인 처리로 예를들어 A라는 작업이 끝난 후 B라는작업, C라는 작업 등 순차적으로 작업을 수행, 작업이 완료될 때 까지 대기해야하는 처리방식입니다. <br>


비동기 <br>
간단히 말해 병렬 처리로, A라는 작업을 요청한뒤, 결과를 기다리지 않고 다음 동작인 C작업을 하는것을 의미합니다. <br>
요청한 작업이 완료될 때 별도로 확인을 해야 하지만 작업이 오래 걸린다 하더라도 다른 작업을 계속할 수 있기 때문에 효율적인 작업이 가능합니다. <br> <br>

사용처
* 게임중 용량이 큰 파일(동영상 등등)을 로드할 때
* SDK나 기타 필요 라이브러리 등을 처음 로드할 때
* 순서가 확실하게 정해져 있는 작업을 할 때

<br>

C++에도 동기 비동기를 사용할 수 있으며, <br>
C#과는 달리 ```std::promise``` , ```std::future``` 이 두가지를 사용하여 동기 비동기처리를 할 수 있습니다. <br>

C++에서 사용하는 동기 비동기 -> [C++ 동기 비동기]()<br><br><br>


### 사용법
--- 
C#에서 동기 처리를 하기위해서는 아래의 2가지 키워드를 알고 있어야합니다.<br>

```c#
async // await키워드를 Method내에서 사용 할 수 있게 만들어주는것
await // 비동기 처리의 흐름을 제어하는 키워드로 실질적인 비동기 작업이 실행되는곳 입니다
```
<br>

async void이렇게도 사용할 수 있으나, 이렇게 사용하면 비동기 메서드를 호출하는 쪽에서 비동기 제어할 수 없으니 가급적 사용하지 않으시기를 추천드립니다. <br>
(다만, 종종 UI버튼 이벤트 등 이벤트 핸들러로 사용할 때 void를 사용하곤 합니다.)<br><br>

사용 예시
```c#
public async void TestAsync()
{
 
}

public async Task TestAsync()
{
	await Task.Delay(1000);
}

public async Task<int> TestAsync()
{
	await Task.Delay(1000);
	return 1;
}
```
<br>

전체적인 코드에서 사용법 예시 입니다. <br>
아래에서 보시다시피 Main스레드에서는 TestAsync를 호출하고 ```await Task.Delay(5000);``` 를 실행하여 내부 타이머를 사용해 스레드 풀의 큐에 들어가게 됩니다. <br>
메인 스레드는 약 5초뒤  ```await Task.Delay(5000);``` 작업이 끝나면 스레드 풀에 있는 잉여 스레드가 End TestAsync를 출력합니다. <br><br><br>


비동기 처리 사용 코드
```c#
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main(string[] args)
    {
        TestAsync();
        Console.WriteLine("End Main, Stand by TestAsync");
    }

    public static async void TestAsync()
    {
        await Task.Delay(5000);
        Console.WriteLine("End TestAsync");
    }
}
```
<br>



동기 처리 사용 코드
```c#
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main(string[] args)
    {
        TestAsync();
        Console.WriteLine("End Main, Stand by TestAsync");
    }

    public static void TestAsync()
    {
        Task.Delay(5000);
        Console.WriteLine("End TestAsync");
    }
}
```
<br>


여기서 5초를 기다리지 않고 End TestAsync 가 출력 된 이유는 ```Task.Delay(5000);``` 의 반환값인 5초 대리 작업을 await하지 않았기 때문입니다.
Task를 await하지 않았기 때문에 프로그램은 5초를 기다리는 작업이 완료 되는것을 기다리지 않고 계속 실행 합니다.


<br>
[Top](#){: .btn .btn--primary }{: .align-right}