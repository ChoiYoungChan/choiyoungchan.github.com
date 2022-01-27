---
title:  "[Unity] Singleton Pattern"
excerpt: Unity에서 사용하는 Singleton Pattern

categories:
  - unity-coding
tags:
  - [Design Pattern, Singleton, Unity, 싱글톤]

toc: true
toc_sticky: true
 
date: 2022-01-15
last_modified_at: 2022-01-15
---

https://choiyoungchan.github.io/design%20pattern/singleton/

싱글톤 패턴의 사용 이유와 개념은 위의 포스팅을 참조

---
## 사용법
---
싱글톤 패턴을 구현하는 방법은 여러가지가 있으나 기본적으로 Static형 인스턴스를 1개 생성한다는점에서 공통점이 있으며, Unity에서 활용 가능한 싱글톤 패턴을 4가지 정도 소개하고자 합니다. <br>
경우와 상황에 따라 변형 하여 사용하는 경우도 많이 있습니다. <br>

- 일반적인 싱글톤
- MonoBehaviour를 사용한 싱글톤
- Generic을 활용, MonoBehaviour를 사용 하는 싱글톤
- Generic을 활용, MonoBehaviour를 사용 하지않는 싱글톤
<br> 

--- 
 <br>

### 일반적인 싱글톤 <br> <br>
![2022-01-16-Singleton](https://user-images.githubusercontent.com/40765022/149659927-65497542-5234-4515-a054-e98f8fe465b8.png) <br><br>

### MonoBehaviour를 사용한 싱글톤 <br>
![2022-01-16-Mono_Singleton](https://user-images.githubusercontent.com/40765022/149660251-ad1282f0-3dcd-40c0-8f59-9205bc52552f.png) <br><br>


### Generic을 활용, MonoBehaviour를 사용 하는 싱글톤 <br>
![2022-01-16_Singleton](https://user-images.githubusercontent.com/40765022/149659385-8cb35339-775e-45b6-88b0-3498424bf232.png) <br><br> 


#### 사용 예시 <br>
![2022-01-16-MonoSingleton_Example](https://user-images.githubusercontent.com/40765022/149659671-fa262214-8984-4723-9846-82f871fbe6f8.png) <br><br>



### Generic을 활용, MonoBehaviour를 사용 하지않는 싱글톤 <br>
![2022-01-16-Generic_No_Mono_Singleton](https://user-images.githubusercontent.com/40765022/149660103-200d6a1c-6fe8-4e95-915d-c52839b293a6.png) <br><br> <br><br> 

---

## 문제점&주의사항
---
- 싱글톤의 역할이 커질 수록 결합도가 높아져서 객체 지향 설계 원칙(개방-폐쇄 원칙)에 어긋날 수 있다.
- 객체의 파괴 시점을 컨트롤 하기 어려워질 수 있다.
- 멀티쓰레드 환경에서 컨트롤이 어렵다.


<br>
[Top](#){: .btn .btn--primary }{: .align-right}