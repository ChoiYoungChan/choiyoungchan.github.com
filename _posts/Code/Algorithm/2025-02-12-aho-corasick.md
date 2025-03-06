---
title:  "[Algorithm] 아호 코라식 알고리즘(Aho Corasick Algorithm) 쉽게 배우기 (C++ 코드 예제 포함)"
excerpt: Aho Corasick Algorithm

categories:
  - Algorithm
tags:
  - [Algorithm, 아호 코라식 알고리즘, Aho Corasick Algorithm, Corasick]

toc: true
toc_sticky: true
 
date: 2025-02-12
last_modified_at: 2025-02-12
---

## 아호 코라식 알고리즘(Aho Corasick Algorithm) 이란?
---
아호-코라식(Aho-Corasick) 알고리즘은 **여러 개의 패턴을 한 번의 탐색으로 찾을 수 있는 문자열 검색 알고리즘** 입니다.
이 알고리즘은 **트라이(Trie)** + **실패 연결(Failure Link)** 을 사용하여 ***KMP 알고리즘을 확장한 방식*** 으로 동작합니다.

일반적인 문자열 검색 알고리즘(예: KMP)은 하나의 패턴만 찾을 수 있지만, 아호-코라식 알고리즘은 **여러 개의 패턴을 동시**에 찾을 수 있습니다.
따라서 스팸 필터링, DNA 서열 분석, 네트워크 패킷 분석과 같은 분야에서 널리 사용됩니다.

1. 트라이(Trie) 구성
   * 여러 개의 패턴을 저장하기 위해 **트라이 자료구조**를 사용합니다.
   * 패턴의 각 문자를 트리 노드로 저장합니다.
   * 패턴의 끝 부분에는 "출력(output)" 정보를 추가하여 매칭된 패턴을 추적할 수 있도록 합니다.

1. 실패 연결(Failure Link) 생성
   * KMP 알고리즘의 LPS(Longest Prefix Suffix) 배열과 유사한 개념입니다.
   * 한 노드에서 일치하는 문자가 없을 경우, 이동할 수 있는 **가장 긴 접두사(prefix) 위치**를 연결합니다.
   * 이를 통해 실패 발생 시, 즉시 다른 경로로 이동하여 검색 속도를 향상시킵니다.

2. 트라이를 사용한 문자열 검색
   * 텍스트를 처음부터 끝까지 탐색하면서, 트라이에서 일치하는 경로를 따라 이동합니다.
   * 만약 일치하는 경로가 없다면, 실패 연결(Failure Link)을 따라 이동하여 다시 검색을 시도합니다.
   * 패턴이 완전히 매칭될 경우, 출력(output) 정보를 이용하여 어떤 패턴이 검색되었는지 확인합니다.
<br><br>

![Image](https://github.com/user-attachments/assets/fd4a1f86-d895-4760-bd27-25acc6ce361b)<br>
(출처 : https://en.wikipedia.org/wiki/Aho%E2%80%93Corasick_algorithm)
<br><br>

### 아호 코라식 알고리즘 동작 과정

[예제]
```
패턴 목록: ["he", "she", "his", "hers"]
텍스트: "ahishers"
```

🔹 1. 트라이(Trie) 구성
각 패턴을 트라이에 삽입하면 다음과 같은 구조가 됩니다.
```
          (root)
         /   |   \
        h    s    (fail)
       / \    \
      e   i    h
     /    |     \
    r     s      e
    |            |
    s            r

```
* "he" → "h" → "e" (패턴 끝)
* "she" → "s" → "h" → "e" (패턴 끝)
* "his" → "h" → "i" → "s" (패턴 끝)
* "hers" → "h" → "e" → "r" → "s" (패턴 끝)
<br><br>

🔹 2. 실패 연결(Failure Link) 구성
실패 연결을 설정하면 다음과 같은 트리가 됩니다.
```
          (root)
         /   |   \
        h    s    (fail)
       / \    \
      e → s    h
     /    |     \
    r →   i      e
    |            |
    s →   s →   r

```
* "h"의 실패 연결은 루트("")로 설정됩니다.
* "s"의 실패 연결도 루트로 설정됩니다.
* "e"의 실패 연결은 "s"로 설정됩니다.
* "r"의 실패 연결은 "s"로 설정됩니다.
* "s"의 실패 연결은 "e"로 설정됩니다.
<br><br>

🔹 3. 텍스트에서 패턴 검색
텍스트 "ahishers"에서 검색을 수행하면 다음과 같습니다.
```
텍스트:   "ahishers"
트라이 경로: (fail) → "h" → "i" → "s" (match: "his") → "h" → "e" → "r" → "s" (match: "hers")
```
<br>

### 장단점
---
#### 장점
* 여러 개의 패턴을 한 번에 검색 가능
  * 일반적인 문자열 검색 알고리즘(예: KMP, Boyer-Moore)은 하나의 패턴만 검색하지만, 아호-코라식 알고리즘은 여러 개의 패턴을 동시에 검색할 수 있습니다.
  * 따라서 스팸 필터링, 악성 코드 탐지, 네트워크 보안 등에서 효율적으로 사용됩니다.

* 선형 시간 복잡도 (O(N + M))
  * N: 텍스트 길이, M: 패턴 길이 총합
  * 검색 과정에서 한 번의 탐색으로 여러 패턴을 찾을 수 있어 매우 빠릅니다.
  * 일반적인 브루트포스(naive) 검색(O(N * M))보다 훨씬 효율적입니다.

* KMP의 LPS(Failure Function) 개념을 확장
  * 실패 연결(Failure Link)을 사용하여 일치하지 않는 경우에도 최대한 많이 이동합니다.
  * 따라서 불필요한 비교를 줄일 수 있어 검색 속도가 빠릅니다.

* 트라이(Trie) 구조를 활용한 검색 최적화
  * 트라이를 사용하여 빠른 탐색이 가능하며, 한 번 구축하면 여러 개의 문자열을 효율적으로 탐색할 수 있습니다.
  * 따라서 사전(dictionary) 기반 검색, 자동 완성 기능 등에 활용됩니다.

* 유니코드(Unicode) 및 다양한 문자 집합 지원 가능
  * 트라이의 키를 확장하면 한글, 일본어, 중국어 등 여러 문자 집합을 지원할 수 있습니다.
  * 따라서 다국어 텍스트 처리에도 적합합니다.

#### 단점
* 메모리 사용량이 큼 (O(M * Σ))
  * 트라이(Trie) 구조를 사용하기 때문에 메모리 사용량이 많을 수 있습니다.
  * 특히, 패턴이 많거나 문자의 종류(Σ, 알파벳 크기)가 클 경우 메모리 부담이 증가합니다.
  * 해결책: 트라이를 압축하여(Compact Trie, DAWG) 메모리 사용을 최적화할 수 있음.

* 구현이 복잡함
  * 단순한 문자열 검색 알고리즘(KMP, Rabin-Karp)보다 구현이 어렵습니다.
  * 트라이 구축, 실패 연결(Failure Link) 설정, 검색 과정 등이 필요하기 때문에 코드 길이가 길어질 수 있습니다.

* 트라이 구축에 시간이 걸림 (O(M))
  * 패턴이 많을수록 트라이를 구축하는 데 시간이 오래 걸릴 수 있습니다.
  * 하지만, 한 번 구축하면 여러 번 사용할 수 있어 검색은 빠르게 수행됩니다.

* 패턴이 많아지면 트라이 탐색 속도가 감소할 수 있음
  * 트라이에 저장된 패턴 수가 많아지면 탐색 과정에서 여러 번 이동해야 하는 경우가 발생할 수 있습니다.
  * 해결책: 트라이 최적화(압축 트라이, Double-Array Trie) 및 병렬 처리 기법 사용 가능.

* 단순한 검색에는 오버헤드가 있을 수 있음
  * 하나의 패턴만 검색하는 경우, KMP 또는 Boyer-Moore 알고리즘이 더 효율적일 수 있습니다.
  * 따라서, 패턴 개수가 적으면 굳이 아호-코라식을 사용할 필요가 없습니다.
<br>

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
<br>

## 예제
---

[트라이(Trie) 구축, 실패 연결(Failure Link) 설정, 문자열 검색을 수행합니다.]
```c++
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

class AhoCorasick {
private:
    struct TrieNode {
        unordered_map<char, TrieNode*> children;
        TrieNode* fail; // 실패 연결(Failure Link)
        vector<string> output; // 매칭된 패턴 저장

        TrieNode() : fail(nullptr) {}
    };

    TrieNode* root;

public:
    AhoCorasick() {
        root = new TrieNode();
    }

    // 트라이(Trie)에 패턴 삽입
    void insertPattern(const string& pattern) {
        TrieNode* node = root;
        for (char c : pattern) {
            if (!node->children.count(c)) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
        }
        node->output.push_back(pattern); // 패턴 끝에 output 추가
    }

    // 실패 연결(Failure Link) 설정
    void buildFailureLinks() {
        queue<TrieNode*> q;
        root->fail = root;
        
        for (auto& [key, child] : root->children) {
            child->fail = root;
            q.push(child);
        }

        while (!q.empty()) {
            TrieNode* node = q.front();
            q.pop();

            for (auto& [key, child] : node->children) {
                TrieNode* failNode = node->fail;

                while (failNode != root && !failNode->children.count(key)) {
                    failNode = failNode->fail;
                }

                if (failNode->children.count(key)) {
                    child->fail = failNode->children[key];
                } else {
                    child->fail = root;
                }

                child->output.insert(child->output.end(), child->fail->output.begin(), child->fail->output.end());
                q.push(child);
            }
        }
    }

    // 텍스트에서 패턴 검색
    void search(const string& text) {
        TrieNode* node = root;

        for (int i = 0; i < text.size(); i++) {
            while (node != root && !node->children.count(text[i])) {
                node = node->fail;
            }

            if (node->children.count(text[i])) {
                node = node->children[text[i]];
            }

            for (const string& pattern : node->output) {
                cout << "패턴 '" << pattern << "'이(가) 인덱스 " << (i - pattern.size() + 1) << "에서 발견됨.\n";
            }
        }
    }
};

int main() {
    AhoCorasick ac;
    vector<string> patterns = {"he", "she", "his", "hers"};
    string text = "ahishers";

    for (const string& pattern : patterns) {
        ac.insertPattern(pattern);
    }

    ac.buildFailureLinks();
    ac.search(text);

    return 0;
}

```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}