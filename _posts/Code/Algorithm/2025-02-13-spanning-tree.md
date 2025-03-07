---
title:  "[Algorithm] 스패닝 트리 알고리즘(Spanning Tree Algorithm) 쉽게 배우기 (C# 코드 예제 2개 포함)"
excerpt: Greedy Algorithm

categories:
  - Algorithm
tags:
  - [Algorithm, 그리디 알고리즘, Spanning Tree Algorithm, Spanning Tree]

toc: true
toc_sticky: true
 
date: 2025-02-13
last_modified_at: 2025-02-13
---

## 스패닝 트리 알고리즘(Spanning Tree Algorithm) 이란?
---
스패닝 트리(Spanning Tree)는 연결 그래프(Connected Graph)에서 모든 정점을 포함하면서 사이클이 없는 최소 연결 부분 그래프입니다.<br>
즉, 그래프의 모든 정점을 포함하면서 최소한의 간선으로 연결한 트리입니다.<br>

📌 N개의 정점을 가진 그래프에서 (N-1)개의 간선으로 이루어진 트리<br>
📌 모든 정점이 연결되며, 사이클이 존재하지 않음<br>
📌 원래 그래프의 모든 정점을 포함하지만, 간선 수를 최소화하여 최소 연결성을 유지<br>
<br>

최소 신장 트리(MST, Minimum Spanning Tree)란?<br>
📌 모든 정점을 연결하면서 가중치 합이 최소가 되는 트리<br>
📌 대표적인 최소 신장 트리 알고리즘:<br>
📌 크루스칼 알고리즘(Kruskal's Algorithm) → 간선을 기준으로 정렬<br>
📌 프림 알고리즘(Prim's Algorithm) → 정점을 기준으로 확장<br>
<br>

![Image](https://github.com/user-attachments/assets/9502cf15-6658-478c-b72b-d216d0f3cd9d)<br>
(출처 : https://www.geeksforgeeks.org/spanning-tree/)
<br><br>

### 스패닝 트리의 주요 알고리즘
---
#### 크루스칼 알고리즘 (Kruskal’s Algorithm)

📌 핵심 개념
* 간선 중심 접근 방식: 모든 간선을 가중치 기준 오름차순 정렬
* 사이클을 방지하기 위해 유니온-파인드(Union-Find) 사용
* 시간 복잡도: O(E log E), 간선 정렬이 주요 연산

(참조 : https://choiyoungchan.github.io/algorithm/kruskal/)

[샘플 코드]
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class DisjointSet {
public:
    vector<int> parent, rank;
    
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // 경로 압축(Path Compression)
        return parent[x];
    }

    void unite(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY])
                parent[rootY] = rootX;
            else if (rank[rootX] < rank[rootY])
                parent[rootX] = rootY;
            else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};

struct Edge {
    int u, v, weight;
    bool operator<(const Edge &other) const {
        return weight < other.weight; // 가중치 기준 정렬
    }
};

vector<Edge> kruskal(int n, vector<Edge> &edges) {
    sort(edges.begin(), edges.end()); // 간선 가중치 기준 정렬
    DisjointSet ds(n);
    vector<Edge> mst;
    
    for (const auto &edge : edges) {
        if (ds.find(edge.u) != ds.find(edge.v)) { // 사이클 방지
            ds.unite(edge.u, edge.v);
            mst.push_back(edge);
        }
    }
    return mst;
}

int main() {
    int n = 4; // 정점 개수
    vector<Edge> edges = {
        {0, 1, 1}, {1, 2, 2}, {0, 2, 3}, {2, 3, 4}, {1, 3, 5}
    };

    vector<Edge> mst = kruskal(n, edges);

    cout << "MST 간선 목록:\n";
    for (const auto &edge : mst)
        cout << edge.u << " - " << edge.v << " (가중치: " << edge.weight << ")\n";

    return 0;
}
```
<br><br>

#### 프림 알고리즘 (Prim’s Algorithm)

📌 핵심 개념
* 정점 중심 접근 방식: 하나의 정점에서 출발하여 최소 비용 간선을 확장
* 우선순위 큐(priority_queue) 사용 → 최소 가중치 간선을 빠르게 선택
* 시간 복잡도: O(E log V), 우선순위 큐를 활용한 탐색

(참조 : https://choiyoungchan.github.io/algorithm/prim/)

[샘플 코드]
```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

typedef pair<int, int> pii; // (가중치, 정점)

vector<pair<int, int>> prim(int n, vector<vector<pii>> &adj) {
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    vector<bool> visited(n, false);
    vector<pair<int, int>> mst;
    
    pq.push({0, 0}); // (가중치, 시작 정점)

    while (!pq.empty()) {
        auto [weight, u] = pq.top();
        pq.pop();

        if (visited[u]) continue;
        visited[u] = true;

        if (u != 0) // 시작 정점은 제외
            mst.push_back({u, weight});

        for (auto [v, w] : adj[u]) {
            if (!visited[v]) {
                pq.push({w, v});
            }
        }
    }
    return mst;
}

int main() {
    int n = 4; // 정점 개수
    vector<vector<pii>> adj(n);
    
    // 인접 리스트 (정점 u -> (v, 가중치))
    adj[0].push_back({1, 1});
    adj[0].push_back({2, 3});
    adj[1].push_back({0, 1});
    adj[1].push_back({2, 2});
    adj[1].push_back({3, 5});
    adj[2].push_back({0, 3});
    adj[2].push_back({1, 2});
    adj[2].push_back({3, 4});
    adj[3].push_back({1, 5});
    adj[3].push_back({2, 4});

    vector<pair<int, int>> mst = prim(n, adj);

    cout << "MST 간선 목록:\n";
    for (auto &[u, w] : mst)
        cout << "정점: " << u << " (가중치: " << w << ")\n";

    return 0;
}
```
<br>

#### 크루스칼 vs 프림 알고리즘 비교

![Image](https://github.com/user-attachments/assets/58203b66-4740-4dbe-a633-8434fcea4969)
<br><br>

### 장단점
---
#### 장점
* 최소 비용으로 모든 정점 연결 가능
* 사이클 없이 네트워크를 구축할 수 있음
* 최소한의 간선으로 효율적인 그래프 구성 가능
* 연결 그래프에서 항상 존재하는 해(解) 보장

#### 단점
* 트리 구조라서 경로 최적화는 아님 → 최단 경로 탐색을 원하면 다익스트라(Dijkstra)나 플로이드-워셜(Floyd-Warshall) 알고리즘 필요
* 정점 추가/제거 시 다시 계산해야 함
* 간선의 가중치가 변하면 트리를 다시 구성해야 함
<br><br>

### 사용 구분
---
#### 아호-코라식 알고리즘이 적합한 경우
✅ 여러 개의 패턴을 한 번에 검색해야 할 때<br>
✅ 사전(dictionary) 검색, 스팸 필터링, 악성 코드 탐지 등에 활용할 때<br>
✅ 텍스트가 길고 검색을 반복해야 할 때<br>
✅ KMP처럼 선형 시간(O(N + M)) 내 검색이 필요한 경우<br>

#### 아호-코라식보다 다른 알고리즘이 나은 경우
❌ 검색할 패턴이 1~2개뿐인 경우 → KMP, Boyer-Moore 사용 추천<br>
❌ 메모리 사용이 중요한 환경 (임베디드 시스템 등) → Rabin-Karp 사용 가능<br>
❌ 검색 대상이 작은 경우 → 단순한 브루트포스 검색으로 충분할 수도 있음<br>
<br>

### 시간 복잡도
---
* 트라이 구축: O(M) (M: 패턴 문자열 길이 총합)
* 실패 연결(Failure Link) 구축: O(M)
* 문자열 검색: O(N) (N: 텍스트 길이)

➡ 최종 시간 복잡도: O(N + M)
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}