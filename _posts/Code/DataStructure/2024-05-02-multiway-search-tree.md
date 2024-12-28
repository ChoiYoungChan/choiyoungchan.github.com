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

## 다원 탐색 트리 란?
---
다원 탐색 트리(Multiway Search Tree) 또는 m-원 탐색 트리(m-way search tree)는 다음과 같은 특징을 갖는 트리입니다.<br>

* 하나의 노드는 최대 m-1개의 키(key)와 m개의 자식(child)을 가질 수 있습니다. 여기서 m은 트리의 차수(order)라고 합니다.
* 각 노드 안의 키는 오름차순으로 정렬되어 있습니다.
* 노드의 키 Ki와 Ki+1 사이의 서브 트리에 있는 모든 값은 Ki보다 크고 Ki+1보다 작습니다
* 모든 리프 노드는 같은 깊이를 가집니다. (균형 트리)

이진 탐색 트리는 m=2인 다원 탐색 트리의 특수한 경우입니다.<br><br>

![MultiwaySearchTree](https://github.com/user-attachments/assets/263061a1-5a57-44ae-b19c-7dd7f72a2795)<br>
(이미지출처 geeksforgeeks)
<br><br>

### 특징
* 높이 감소: 하나의 노드가 여러 개의 키를 가질 수 있기 때문에, 같은 수의 데이터를 저장하는 이진 탐색 트리에 비해 트리의 높이가 낮아집니다. 이는 디스크 접근 횟수를 줄여 성능 향상에 도움이 됩니다.
* 균형 유지: 모든 리프 노드가 같은 깊이를 가지므로, 트리의 균형이 유지됩니다. 이를 통해 탐색, 삽입, 삭제 연산의 시간 복잡도가 보장됩니다.
* 외부 저장 장치에 적합: 하나의 노드를 디스크의 하나의 블록에 저장하여 디스크 I/O 횟수를 최소화할 수 있습니다.

<br><br>

### 다원 탐색 트리의 종류
---
* B-트리 (B-tree): 가장 널리 사용되는 다원 탐색 트리 중 하나입니다. 각 노드의 키 개수에 최소 개수와 최대 개수에 대한 제약이 있습니다.
* B+ 트리 (B+ tree): B-트리의 변형으로, 모든 데이터를 리프 노드에 저장하고, 리프 노드들을 연결 리스트로 연결하여 순차 접근을 효율적으로 지원합니다. 데이터베이스 인덱싱에 주로 사용됩니다.
* B* 트리 (B* tree): B-트리의 또 다른 변형으로, 형제 노드 간의 키 공유를 통해 공간 활용률을 높입니다.

<br><br>

### 장단점
---
#### 장점
* 효율적인 대용량 데이터 관리: 디스크 I/O 횟수를 최소화하여 대용량 데이터 처리에 적합합니다.
* 빠른 탐색, 삽입, 삭제: 균형 트리이므로 O(log n)의 시간 복잡도를 보장합니다.

#### 단점
* 구현 복잡: 삽입, 삭제, 분할 등의 연산 구현이 비교적 복잡합니다.
* 메모리 오버헤드: 각 노드에 여러 개의 키와 자식 포인터를 저장해야 하므로, 메모리 사용량이 증가할 수 있습니다.

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