---
title:  "[Algorithm] 백 트래킹(Backtracking)"
excerpt: Backtracking

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 백 트래킹, Backtracking]

toc: true
toc_sticky: true
 
date: 2023-09-05
last_modified_at: 2023-09-05
---

## 백 트래킹(Backtracking)개념
---
백트래킹은 "되추적"이라고도 하며, 문제의 해를 찾기 위해 탐색 공간을 체계적으로 탐색하는 알고리즘입니다. 탐색 과정에서 현재 경로가 해답으로 이어질 가능성이 없다고 판단되면, 즉시 이전 단계로 돌아가 다른 경로를 탐색합니다. <br><br>
이러한 방식으로 불필요한 탐색을 줄여 효율성을 향상시킵니다. 마치 미로 찾기에서 막다른 길에 다다르면 왔던 길을 되돌아가 다른 길을 찾는 것과 유사합니다.

<br><br>

### 백 트래킹(Backtracking)동작 방식
---
* 상태 공간 트리 (State Space Tree): 문제의 가능한 모든 상태를 트리 형태로 나타냅니다. 각 노드는 문제의 부분적인 해 또는 상태를 나타내고, 간선은 상태 변화를 나타냅니다.
* 깊이 우선 탐색 (DFS): 상태 공간 트리를 깊이 우선 방식으로 탐색합니다. 즉, 한 경로를 끝까지 탐색해보고, 해답을 찾지 못하면 이전 단계로 돌아가 다른 경로를 탐색합니다
* 가지치기 (Pruning): 탐색 도중 현재 경로가 해답으로 이어질 가능성이 없다고 판단되면, 해당 경로의 하위 노드들을 더 이상 탐색하지 않고 이전 단계로 돌아갑니다. 이를 가지치기라고 하며, 백트래킹의 핵심적인 부분입니다.

### 백 트래킹(Backtracking)의 장단점
---
#### 장점
* 모든 가능한 해를 탐색하기 때문에, 해가 존재한다면 반드시 찾을 수 있습니다.
* 가지치기를 통해 불필요한 탐색을 줄여 탐색 시간을 단축할 수 있습니다.

#### 단점
* 모든 경우의 수를 탐색하는 완전 탐색(Brute Force)에 비해 효율적이지만, 문제의 크기가 커지면 여전히 많은 시간이 소요될 수 있습니다.
* 가지치기 조건을 명확하게 정의하고 구현하는 것이 어려울 수 있습니다.

<br><br>

### 백 트래킹(Backtracking) 활용 예시
---
* N-Queens 문제: N개의 퀸을 체스판에 서로 공격하지 않도록 배치하는 문제.
* 스도쿠 (Sudoku): 9x9 격자에 숫자를 채우는 퍼즐.
* 조합 (Combination): 주어진 집합에서 특정 개수의 원소를 선택하는 문제.
* 부분 집합 (Subset): 주어진 집합의 모든 부분 집합을 찾는 문제.
* 순열 (Permutation): 주어진 원소들을 나열하는 모든 경우의 수를 찾는 문제.
* 미로 찾기 (Maze Solving): 미로에서 출구를 찾는 문제.

## 예제
---

[N-Queens 문제]<br>
``` C++
#include <iostream>
#include <vector>

using namespace std;

int n;
vector<int> col; // col[i]는 i번째 행에 놓인 퀸의 열 위치

bool isSafe(int row) {
    for (int i = 0; i < row; i++) {
        if (col[i] == col[row] || abs(col[i] - col[row]) == row - i) {
            return false; // 같은 열 또는 대각선에 퀸이 있는 경우
        }
    }
    return true;
}

void nQueens(int row) {
    if (row == n) {
        // 모든 퀸을 배치한 경우 출력
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (col[i] == j) {
                    cout << "Q ";
                } else {
                    cout << ". ";
                }
            }
            cout << endl;
        }
        cout << endl;
        return;
    }

    for (int i = 0; i < n; i++) {
        col[row] = i;
        if (isSafe(row)) {
            nQueens(row + 1); // 다음 행 탐색
        }
    }
}

int main() {
    cout << "N을 입력하세요: ";
    cin >> n;

    col.resize(n);
    nQueens(0); // 0번째 행부터 시작

    return 0;
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}