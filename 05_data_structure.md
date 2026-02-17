# 제5장. 자료구조 (Data Structure)

> **[심화] (Deep Dive)** 섹션이 추가되었습니다.

## 📌 왜 배워야 하나요? (Why?)
자료구조는 **데이터를 효율적으로 저장하고 관리하는 방법**입니다. 상황에 맞는 적절한 자료구조를 선택해야 **시간 복잡도(Time Complexity)**와 **공간 복잡도(Space Complexity)**를 최적화하여 서비스 성능을 높일 수 있습니다. (예: 검색이 잦으면 Hash Table, 순서가 중요하면 Queue)

---

## 1. 알고리즘과 복잡도

### 🕒 시간 복잡도 (Time Complexity)
입력 크기(N)에 따라 알고리즘 실행 시간이 얼마나 걸리는지 나타내는 척도입니다. 주로 **빅오(Big-O) 표기법**을 사용합니다.

*   **O(1)**: 상수 시간. 입력 크기와 무관. (예: 배열 인덱스 접근, 스택 Push/Pop)
*   **O(log N)**: 로그 시간. 한 번 수행할 때마다 탐색 범위가 절반으로 줄어듦. (예: 이진 탐색)
*   **O(N)**: 선형 시간. 입력 크기만큼 반복. (예: for 문 하나)
*   **O(N log N)**: 선형 로그 시간. 효율적인 정렬 알고리즘. (예: Merge Sort, Quick Sort, Heap Sort)
*   **O(N^2)**: 이차 시간. 이중 for 문. (예: Bubble Sort)

---

## 2. 선형 자료구조 (Linear)

데이터가 일렬로 나열된 형태입니다.

### 🍱 배열 (Array) vs 연결 리스트 (Linked List)
*   **배열 (Array)**:
    *   논리적 순서와 물리적(메모리) 순서가 일치합니다.
    *   **접근(Access)**: 인덱스로 접근하므로 빠름 **O(1)**.
    *   **삽입/삭제**: 중간 데이터를 밀거나 당겨야 하므로 느림 **O(N)**.
*   **연결 리스트 (Linked List)**:
    *   노드(Node)가 다음 노드의 주소를 가리키며 연결됩니다.
    *   **접근**: 처음부터 찾아가야 하므로 느림 **O(N)**.
    *   **삽입/삭제**: 주소만 바꾸면 되므로 빠름 **O(1)** (단, 위치를 알고 있을 때).

---

## 3. 스택과 큐 (Stack & Queue)

### 🥞 스택 (Stack)
*   **LIFO (Last-In First-Out)**: 나중에 들어온 놈이 먼저 나갑니다.
*   **용도**: 함수 호출 스택, 뒤로 가기, 괄호 검사. (`push`, `pop`)

### 🎫 큐 (Queue)
*   **FIFO (First-In First-Out)**: 먼저 들어온 놈이 먼저 나갑니다.
*   **용도**: 작업 대기열(Printer Queue), BFS 탐색. (`enqueue`, `dequeue`)

---

## 4. 비선형 자료구조 (Non-linear)

### 🌲 트리 (Tree)
계층적 구조를 나타냅니다. (부모-자식 관계)
*   **이진 탐색 트리 (BST)**: 왼쪽 자식 < 부모 < 오른쪽 자식 규칙을 만족. 탐색 **O(log N)**.
*   **힙 (Heap)**: 최댓값이나 최솟값을 빠르게 찾아내기 위한 완전 이진 트리. (우선순위 큐 구현에 사용)

### 🕸️ 그래프 (Graph)
정점(Vertex)과 간선(Edge)으로 이루어진 구조입니다.
*   **DFS (깊이 우선 탐색)**: 스택이나 재귀 사용. 한 우물만 깊게 팜. (미로 찾기)
*   **BFS (너비 우선 탐색)**: 큐 사용. 가까운 곳부터 탐색. (최단 경로 찾기)

---

## 5. 해시 테이블 (Hash Table)

Key-Value 쌍으로 데이터를 저장하는 구조입니다.
*   **해시 함수(Hash Function)**를 통해 Key를 고유한 인덱스로 변환합니다.
*   **충돌(Collision)**: 서로 다른 Key가 같은 인덱스로 변환되는 경우.
    *   **체이닝 (Chaining)**: 연결 리스트로 줄줄이 매답 니다.
    *   **개방 주소법 (Open Addressing)**: 비어있는 옆자리를 찾아갑니다.

### 🐍 Python Example (Dictionary is Hash Table)
```python
phone_book = {}
phone_book["Alice"] = "010-1234-5678" # O(1)
print(phone_book["Alice"]) # O(1)
```

---

## 🎓 Data Engineer & ML Interview Q&A

**Q1. `ArrayList`와 `LinkedList`의 차이점을 설명하고, 각각 언제 써야 하는지 말해보세요.**
> **A.** `ArrayList`는 인덱스를 통한 **랜덤 접근(Random Access)**이 빈번할 때 유리합니다 (O(1)). 반면 `LinkedList`는 리스트의 **중간 위치에서 데이터 삽입, 삭제**가 빈번할 때 유리합니다 (O(1)). 데이터 크기가 가변적이고 삽입/삭제가 많다면 Linked List를, 데이터 크기가 예측 가능하고 조회가 많다면 ArrayList를 추천합니다.

**Q2. 해시 테이블(Hash Table)의 검색 시간 복잡도는 항상 O(1)인가요?**
> **A.** 평균적으로는 **O(1)**이지만, **해시 충돌(Collision)**이 많이 발생하면 최악의 경우 **O(N)**까지 성능이 저하될 수 있습니다. 이를 방지하기 위해 좋은 해시 함수를 사용하고, 충돌 발생 시 체이닝이나 개방 주소법 등으로 적절히 처리해야 합니다. Java 8 이상에서는 체이닝 시 연결 리스트 대신 Red-Black Tree를 사용하여 O(log N)을 보장하기도 합니다.

**Q3. 스택(Stack) 두 개로 큐(Queue)를 구현해 보세요. (알고리즘 질문)**
> **A.** (구두 설명)
> `inStack`과 `outStack` 두 개를 둡니다.
> 1. `enqueue` 시에는 무조건 `inStack`에 `push`합니다.
> 2. `dequeue` 시에는 먼저 `outStack`이 비어있는지 확인합니다.
> 3. 만약 `outStack`이 비어있다면 `inStack`에 있는 모든 데이터를 `pop`하여 `outStack`으로 `push`합니다 (순서가 뒤집힘).
> 4. 그리고 `outStack`에서 `pop`하면 FIFO 순서로 데이터가 나옵니다.

---

## 🔬 Deep Dive: 알고리즘의 극한 효율

### 1. 고급 트리 구조 (Advanced Trees)
*   **Red-Black Tree**: 자가 균형 이진 탐색 트리(Self-Balancing BST)의 대표주자.
    *   **규칙**: 모든 노드는 Red/Black, 루트는 Black, Red의 자식은 Black (No double Red).
    *   **특징**: AVL 트리보다 균형을 덜 엄격하게 맞추지만, 삽입/삭제 시 **회전(Rotation)** 수가 적어 실무(Java HashMap, Linux CFS, C++ Map)에서 더 많이 쓰입니다.
*   **Trie (Prefix Tree)**: 문자열 검색에 특화된 트리. 검색어 자동완성에 사용됩니다. 시간 복잡도는 문자열 길이인 **O(L)**입니다.

### 2. 그래프 최단 경로 알고리즘 비교
*   **Dijkstra**: **음수 가중치**가 없을 때 사용. 우선순위 큐(Heap)를 사용하면 **O(E log V)**. (네비게이션)
*   **Bellman-Ford**: **음수 가중치**가 있을 때 사용. 모든 간선을 V-1번 확인하므로 느림 **O(VE)**. 음수 사이클 탐지 가능.
*   **Floyd-Warshall**: **모든 정점 쌍** 간의 최단 경로. 3중 for문 사용 **O(V^3)**. 구현이 매우 간단.

### 3. 해시 충돌 해결의 디테일
"체이닝하면 끝 아닌가요?" -> 아닙니다.
*   **Linear Probing (선형 조사)**: 충돌 나면 옆 칸 확인. **Cache Hit**율이 좋지만, 데이터가 뭉치는 **Clustering** 문제가 발생합니다.
*   **Open Addressing의 삭제**: 삭제된 공간을 그냥 비우면 탐색이 끊기므로, `DELETED`라는 마킹(Dummy)을 해야 합니다.
*   **Resizing**: 데이터가 꽉 차면 배열 크기를 2배로 늘리고 **모든 데이터를 다시 해싱(Re-hashing)**해야 합니다. (매우 비싼 연산)

### 4. 정렬의 내부 (Sorting Internals)
`sort()` 함수는 어떤 알고리즘을 쓸까요?
*   **Quick Sort**: 평균 O(N log N)이지만, 최악(이미 정렬된 경우) O(N^2). 피벗(Pivot) 선택이 중요합니다 (Randomized Quick Sort).
*   **Merge Sort**: 항상 O(N log N) 보장. 안정 정렬(Stable Sort). 추가 메모리 O(N) 필요.
*   **Tim Sort**: Python과 Java의 기본 정렬. **Merge Sort + Insertion Sort**의 하이브리드. 실생활 데이터는 이미 부분적으로 정렬되어 있다는 점(Run)을 이용해 최적화합니다.