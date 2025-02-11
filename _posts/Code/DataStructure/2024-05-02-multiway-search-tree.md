---
title:  "[Data Structure] 다원 탐색 트리(Multiway Search Tree)"
excerpt: multiway-search-tree

categories:
  - Data Structure
tags:
  - [datastructure, 다원 탐색 트리, Multiway Search Tree]

toc: true
toc_sticky: true
 
date: 2024-05-02
last_modified_at: 2024-05-02
---

## 다원 탐색 트리(Multiway Search Tree) 란?
---
다원 탐색 트리(Multiway Search Tree) 또는 m-원 탐색 트리(m-way search tree)는 하나의 노드가 여러 개의 키(key)와 자식(child)을 가질 수 있는 트리입니다. 이진 탐색 트리가 각 노드당 최대 2개의 자식을 갖는 것과 달리, 다원 탐색 트리는 각 노드당 여러 개의 자식을 가질 수 있습니다. 여기서 m은 트리의 **차수(order)**라고 합니다.<br>

* 하나의 노드는 최대 m-1개의 키(key)와 m개의 자식(child)을 가질 수 있습니다. 여기서 m은 트리의 차수(order)라고 합니다.
* 각 노드 안의 키는 오름차순으로 정렬되어 있습니다.
* 노드의 키 Ki와 Ki+1 사이의 서브 트리에 있는 모든 값은 Ki보다 크고 Ki+1보다 작습니다
* 모든 리프 노드는 같은 깊이를 가집니다. (균형 트리)

이진 탐색 트리는 m=2인 다원 탐색 트리의 특수한 경우입니다.<br><br>

![MultiwaySearchTree](https://github.com/user-attachments/assets/263061a1-5a57-44ae-b19c-7dd7f72a2795)<br>
(이미지출처 geeksforgeeks)
<br><br>

### 특징
* 키와 자식: 하나의 노드는 최대 m-1개의 키(key)와 m개의 자식(child)을 가질 수 있습니다. 키는 노드 안에서 오름차순으로 정렬되어 있으며, 각 키는 자식 노드를 가리키는 포인터를 가지고 있습니다. 마치 책의 목차처럼, 키는 자식 노드를 찾기 위한 역할을 합니다.
* 정렬된 키: 노드 안의 키들은 오름차순으로 정렬되어 있습니다. 이는 탐색 연산을 효율적으로 수행할 수 있도록 도와줍니다. 마치 사전처럼, 키들이 정렬되어 있어 원하는 정보를 빠르게 찾을 수 있습니다.

* 자식 노드와 키의 관계: 노드의 키 Ki와 Ki+1 사이의 서브 트리에 있는 모든 값은 Ki보다 크고 Ki+1보다 작습니다. 이는 이진 탐색 트리의 속성을 일반화한 것으로, 다원 탐색 트리에서도 탐색 연산의 효율성을 보장합니다. 마치 지도에서 지역별 경계선처럼, 키는 자식 노드의 값 범위를 구분하는 역할을 합니다.

* 균형 유지: 모든 리프 노드는 같은 깊이를 가집니다. 이는 트리의 균형을 유지하여 탐색, 삽입, 삭제 연산의 시간 복잡도를 보장합니다. 마치 건물의 균형처럼, 다원 탐색 트리는 균형을 유지하여 안정적인 데이터 관리를 제공합니다.
<br><br>

### 다원 탐색 트리의 종류
---
* B-트리 (B-tree): 가장 널리 사용되는 다원 탐색 트리 중 하나입니다. 각 노드의 키 개수에 최소 개수와 최대 개수에 대한 제약이 있습니다. B-트리는 데이터베이스 인덱싱에 주로 사용됩니다. 마치 도서관의 책 분류 체계처럼, B-트리는 데이터를 효율적으로 관리하고 검색할 수 있도록 도와줍니다.

* B+ 트리 (B+ tree): B-트리의 변형으로, 모든 데이터를 리프 노드에 저장하고, 리프 노드들을 연결 리스트로 연결하여 순차 접근을 효율적으로 지원합니다. B+ 트리 역시 데이터베이스 인덱싱에 주로 사용됩니다. 마치 백과사전처럼, B+ 트리는 데이터 검색과 순차 접근을 모두 효율적으로 지원합니다.

* B* 트리 (B* tree): B-트리의 또 다른 변형으로, 형제 노드 간의 키 공유를 통해 공간 활용률을 높입니다. B* 트리는 B-트리와 B+ 트리의 장점을 결합한 형태입니다. 마치 공유 오피스처럼, B* 트리는 공간 효율성을 높여 데이터를 관리합니다.
<br><br>

### 장단점
---
#### 장점
* 효율적인 대용량 데이터 관리: 디스크 I/O 횟수를 최소화하여 대용량 데이터 처리에 적합합니다. 마치 창고처럼, 다원 탐색 트리는 대량의 데이터를 효율적으로 관리할 수 있습니다.

* 빠른 탐색, 삽입, 삭제: 균형 트리이므로 O(log n)의 시간 복잡도를 보장합니다. 마치 고속도로처럼, 다원 탐색 트리는 데이터를 빠르게 찾고 수정할 수 있습니다.

#### 단점
* 구현 복잡: 삽입, 삭제, 분할 등의 연산 구현이 비교적 복잡합니다. 마치 복잡한 기계 장치처럼, 다원 탐색 트리의 구현은 까다로운 과정을 거쳐야 합니다.

* 메모리 오버헤드: 각 노드에 여러 개의 키와 자식 포인터를 저장해야 하므로, 메모리 사용량이 증가할 수 있습니다. 마치 여러 개의 서랍이 있는 가구처럼, 다원 탐색 트리는 메모리 공간을 더 사용할 수 있습니다.
<br><br>

### 예제
---

```C++
#include <iostream>
#include <vector>
#include <algorithm>

const int M = 3; // 트리의 차수 (M-원 트리)

struct Node {
    std::vector<int> keys;
    std::vector<Node*> children;
    bool isLeaf;

    Node() : isLeaf(true) {}
};

void insertNonFull(Node* node, int key) {
    int i = node->keys.size() - 1;

    if (node->isLeaf) {
        // 리프 노드인 경우 키 삽입
        while (i >= 0 && key < node->keys[i]) {
            node->keys[i + 1] = node->keys[i];
            i--;
        }
        node->keys[i + 1] = key;
    } else {
        // 리프 노드가 아닌 경우 적절한 자식 노드 선택
        while (i >= 0 && key < node->keys[i]) {
            i--;
        }
        i++;

        // 선택된 자식 노드가 가득 차 있는 경우 분할
        if (node->children[i]->keys.size() == M - 1) {
            // splitChild(node, i); // 분할 함수 (구현 생략)
            // 분할 후 다시 적절한 위치 찾기
            if (key > node->keys[i]) {
                i++;
            }
        }
        insertNonFull(node->children[i], key);
    }
}

int main() {
    Node* root = new Node();
    insertNonFull(root, 10);
    insertNonFull(root, 20);
    insertNonFull(root, 30);
    insertNonFull(root, 40);
    insertNonFull(root, 50);

    // ...

    return 0;
}
```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}