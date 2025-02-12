---
title:  "[AI] 병렬 분산 처리(Parallel Distributed Processing)의 기본 개념 정리 (Python 샘플코드 포함)"
excerpt: Parallel Distributed Processing

categories:
  - AI
tags:
  - [AI, 병렬 분산 처리, Parallel Distributed Processing, PDP]

toc: true
toc_sticky: true
 
date: 2024-11-12
last_modified_at: 2024-11-12
---

## 병렬 분산 처리(Parallel Distributed Processing)의 개념
---
PDP는 여러 개의 프로세서를 사용하여 하나의 작업을 동시에 처리하는 것을 의미합니다. 마치 여러 명의 요리사가 함께 요리하는 것처럼, PDP는 여러 개의 프로세서가 협력하여 작업을 빠르게 완료합니다. PDP는 슈퍼컴퓨터, 클라우드 컴퓨팅 등 다양한 분야에서 활용되는 핵심 기술입니다.
<br><br>

![Image](https://github.com/user-attachments/assets/bac5f1a9-533e-4667-81d1-9ba4d0b0b2e8)
(출처 : https://www.researchgate.net/figure/Parallel-distributed-processing-pdp-model-from-Adams-1990-158_fig1_286760498)<br><br>


### 병렬 분산 처리(Parallel Distributed Processing)의 특징
---
* 높은 성능: 여러 개의 프로세서를 사용하여 작업을 동시에 처리하므로, 처리 속도를 획기적으로 향상시킬 수 있습니다.
* 확장성: 필요에 따라 프로세서의 개수를 늘려 성능을 더욱 향상시킬 수 있습니다.
* 분산 처리: 데이터를 여러 개의 프로세서에 분산하여 처리하므로, 대용량 데이터를 효율적으로 처리할 수 있습니다.
* 병렬 처리: 여러 개의 프로세서가 동시에 작업을 처리하므로, 작업 처리 시간을 단축시킬 수 있습니다.
<br><br>

### 병렬 분산 처리(Parallel Distributed Processing)의 종류
---
* 공유 메모리 방식: 여러 개의 프로세서가 공유된 메모리 공간을 사용하여 데이터를 공유하고 통신합니다.
* 분산 메모리 방식: 각 프로세서가 독립적인 메모리 공간을 가지고 있으며, 메시지 교환을 통해 데이터를 공유하고 통신합니다.
<br><br>

### 병렬 분산 처리(Parallel Distributed Processing)의 장단점
---
#### 장점
* 높은 성능: 여러 개의 프로세서를 사용하여 작업 처리 속도를 획기적으로 향상시킬 수 있습니다.
* 확장성: 필요에 따라 프로세서의 개수를 늘려 성능을 더욱 향상시킬 수 있습니다.
* 분산 처리: 대용량 데이터를 효율적으로 처리할 수 있습니다.

#### 단점
* 구현 복잡성: 병렬 처리 및 데이터 분산 등을 고려해야 하므로 구현이 복잡할 수 있습니다.
* 통신 오버헤드: 프로세서 간 통신에 오버헤드가 발생할 수 있습니다.
* 로드 밸런싱: 각 프로세서에 작업을 균등하게 분배하는 것이 중요합니다.
<br><br>

### 병렬 분산 처리(Parallel Distributed Processing)의 과정
---
1. 작업 분할: 하나의 작업을 여러 개의 작은 작업으로 분할합니다. 마치 요리를 하기 위해 재료를 손질하고, 요리하고, 설거지하는 과정을 나누는 것과 같습니다.
2. 작업 할당: 분할된 작업을 여러 개의 프로세서에 할당합니다. 마치 각 요리사에게 재료 손질, 요리, 설거지 중 하나를 맡기는 것과 같습니다.
3. 병렬 처리: 여러 개의 프로세서가 할당된 작업을 동시에 처리합니다. 마치 여러 명의 요리사가 동시에 요리하는 것과 같습니다.
4. 결과 통합: 각 프로세서의 처리 결과를 통합하여 최종 결과를 생성합니다. 마치 모든 요리사의 요리를 합쳐 하나의 완성된 요리를 만드는 것과 같습니다.
<br><br>

```python
import multiprocessing

def worker(num):
    """각 프로세서가 실행할 함수"""
    print(f"Process {num}: 작업 수행")
    # 실제 작업 내용

if __name__ == "__main__":
    processes = []
    for i in range(4): # 4개의 프로세서 생성
        p = multiprocessing.Process(target=worker, args=(i,))
        processes.append(p)
        p.start()

    for p in processes:
        p.join()

    print("모든 작업 완료")
```
<br><br>

### 병렬 분산 처리(Parallel Distributed Processing)의 주의 사항
---
* 병렬 처리 알고리즘: 작업에 적합한 병렬 처리 알고리즘을 선택하는 것이 중요합니다.
* 데이터 분산: 데이터를 효율적으로 분산하는 방법을 고려해야 합니다.
* 프로세스 동기화: 여러 개의 프로세서가 작업을 올바르게 동기화하도록 해야 합니다.
<br><br> 

## 예시
---
[Python, MPI 라이브러리 활용, 분산 메모리 방식]
```python
from mpi4py import MPI

comm = MPI.COMM_WORLD
rank = comm.Get_rank()
size = comm.Get_size()

data = None
if rank == 0:
    data = [1, 2, 3, 4, 5]
    data = [data[i::size] for i in range(size)]

data = comm.scatter(data, root=0)

result = 0
for x in data:
    result += x

result = comm.gather(result, root=0)

if rank == 0:
    print(f"총합: {sum(result)}")
```

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}