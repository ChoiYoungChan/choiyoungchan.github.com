---
title:  "[Algorithm] QuickSort"
excerpt: Unity에서 사용하는 퀵정렬(QuickSort)

categories:
  - Algorithm
tags:
  - [Algorithm, QuickSort, 퀵 정렬, 정렬]

toc: true
toc_sticky: true
 
date: 2022-04-23
last_modified_at: 2022-04-23
---

## 개요
퀵 정렬(Quick Sort)이란?
=> 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법<br> 

정렬하는 과정
1. 리스트 안의 한 요소를 선택한다. 이때 선택한 원로를 피벗(Pivot)이라한다.
2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로, 큰 요소들은 오른쪽으로 옮겨진다.
3. 피벗을 제외한 왼쪽, 오른쪽 리스트를 위의 과정으로 다시 정렬한다.

<br>

![2022-04-23-QuickSort_006](https://user-images.githubusercontent.com/40765022/164965350-02f0ba7c-a474-47ca-89e0-7ccbbea38e0a.gif)

<br>

* 장점
  * 속도가 빠르다.
  * 추가 메모리 공간을 필요로 하지 않는다.

*  단점
   * 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행 시간이 더 많이 걸린다.
 <br>

## 유니테에서 예제
---

### 소스코드
아래는 유니티를 기준으로 작성하였으나 기본적으로 C#이기때문에 숫자를 입력하고 출력하는 부분 외에는 바로 참고하셔도 무방합니다.<br>

[초기화 및 실행함수]<br>
![2022-04-23-QuickSort_000](https://user-images.githubusercontent.com/40765022/164966059-93c6e0f3-0375-4c86-aaa0-c39df0c9c625.png)
<br>

[퀵 정렬]<br>
![2022-04-23-QuickSort_001](https://user-images.githubusercontent.com/40765022/164966071-68b7183f-3ac6-447b-acc5-b4af9e41017d.png)
<br>

[피벗 설정 및 정렬]<br>
![2022-04-23-QuickSort_002](https://user-images.githubusercontent.com/40765022/164966092-e3838f02-b4ca-4ad3-9654-8d1f9a9d0037.png)
<br>

[전체 코드]<br>
![2022-04-23-QuickSort_003](https://user-images.githubusercontent.com/40765022/164965412-6b2090a2-4920-4a13-8af5-ca9b4f1e671e.png)<br>


### 실행 영상
<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Algorithm/Sort/QuickSort_004.mp4" type="video/mp4">
</video>

<br>
<br>

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Algorithm/Sort/QuickSort_005.mp4" type="video/mp4">
</video>
<br>

[Top](#){: .btn .btn--primary }{: .align-right}