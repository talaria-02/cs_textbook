# 📘 신입 DE/ML 전문가를 위한 CS 전공 핵심 총정리

> **"면접관이 물어보는 진짜 CS 지식만 담았습니다."**

이 교과서는 신입 데이터 엔지니어(Data Engineer)와 머신러닝(Machine Learning) 전문가를 목표로 하는 분들을 위해 제작되었습니다. 방대한 전공 서적 내용을 현업 관점에서 재해석하고, 기술 면접에 자주 나오는 핵심 질문을 중심으로 정리했습니다.

## 📚 목차 (Table of Contents)

> **✨ NEW: 각 챕터 마지막에 `심화 학습 (Deep Dive)` 섹션을 추가했습니다.**

### [제1장. 컴퓨터 구조 (Computer Structure)](01_computer_structure.md)
*   폰 노이만 구조와 병목 현상
*   CPU의 작동 원리 (Fetch-Decode-Execute)
*   캐시 메모리와 지역성 (Locality)
*   **[심화]** Pipeline Hazard, Cache Mapping, TLB

### [제2장. 운영체제 (Operating System)](02_OS.md)
*   프로세스 vs 스레드 (Multi-process vs Multi-thread)
*   CPU 스케줄링과 컨텍스트 스위칭
*   데드락(Deadlock)과 동기화(Synchronization)
*   **[심화]** CFS Scheduler, Spinlock/Mutex 내부 구현, IPC 성능 비교

### [제3장. 데이터베이스 (Database)](03_database.md)
*   RDBMS vs NoSQL
*   인덱스(Index)와 조인(Join) 최적화
*   트랜잭션(ACID)과 정규화
*   **[심화]** B-Tree/B+Tree 내부, 격리 수준 이상 현상, MVCC

### [제4장. 네트워크 (Network)](04_network.md)
*   OSI 7계층과 TCP/IP 모델
*   TCP 3-way Handshake와 흐름 제어
*   HTTP/HTTPS와 로드 밸런싱
*   **[심화]** TCP 혼잡 제어(Cubic), HTTP/2&3, TLS Handshake

### [제5장. 자료구조 (Data Structure)](05_data_structure.md)
*   시간 복잡도(Time Complexity)와 공간 복잡도
*   배열, 연결 리스트, 스택, 큐
*   해시 테이블, 트리, 그래프 탐색(DFS/BFS)
*   **[심화]** Red-Black Tree, Advanced Graph Algo, Sorting Internals

## 💡 활용 방법
1.  **빠른 1회독**: 전체적인 흐름을 파악하며 "아, 이런 게 있었지"라고 리마인드합니다.
2.  **면접 질문 답변**: 각 챕터 마지막에 있는 `Interview Q&A`를 보며 입으로 직접 설명해 봅니다.
3.  **심화 학습**: 이해가 부족한 부분은 전공 서적이나 추가 자료를 찾아보며 깊이를 더합니다.
