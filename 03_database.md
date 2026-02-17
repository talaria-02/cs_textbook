# 제3장. 데이터베이스 (Database)

> **[심화] (Deep Dive)** 섹션이 추가되었습니다.

## 📌 왜 배워야 하나요? (Why?)
데이터 엔지니어에게 DB는 가장 기본이 되는 저장소입니다. 단순히 `SELECT`만 하는 것이 아니라, **대용량 트래픽 상황에서 어떻게 데이터 무결성을 유지(Transaction)하고, 조회 속도를 최적화(Index, Partitioning)할 것인가**가 핵심입니다.

---

## 1. 데이터베이스의 큰 그림

### 🔑 핵심 개념
*   **DBMS (Database Management System)**: 데이터를 체계적으로 관리하는 소프트웨어입니다.
*   **RDBMS (Relational DBMS)**: 테이블 형태로 데이터를 저장하고 관계(Relation)를 맺는 **관계형** 데이터베이스 (MySQL, PostgreSQL, Oracle). 엄격한 스키마가 특징입니다.
*   **NoSQL (Not Only SQL)**: 고정된 스키마가 없고 유연하며 확장성이 뛰어난 **비관계형** 데이터베이스 (MongoDB, Redis, Cassandra).

### 🗣️ SQL (Structured Query Language)
데이터베이스와 대화하기 위한 언어입니다.
*   **DDL (Definition)**: 구조 정의 (`CREATE`, `ALTER`, `DROP`)
*   **DML (Manipulation)**: 데이터 조작 (`SELECT`, `INSERT`, `UPDATE`, `DELETE`)
*   **DCL (Control)**: 권한 제어 (`GRANT`, `REVOKE`)
*   **TCL (Transaction Control)**: 트랜잭션 제어 (`COMMIT`, `ROLLBACK`)

---

## 2. RDBMS 구조와 제약 조건

### 🗝️ 키 (Key)와 무결성
*   **기본 키 (Primary Key, PK)**: 테이블에서 각 행(Row)을 **유일하게 식별**하는 키. (NULL 불가, 중복 불가)
*   **외래 키 (Foreign Key, FK)**: 다른 테이블의 PK를 참조하는 키. 테이블 간의 관계를 형성합니다.
*   **무결성 제약 조건 (Integrity Constraint)**:
    *   **개체 무결성**: PK는 NULL일 수 없다.
    *   **참조 무결성**: FK는 참조하는 테이블에 존재하는 값이어야 한다.

---

## 3. 쿼리 효율화 및 최적화

데이터가 많아질수록 쿼리 성능이 시스템 전체의 병목이 됩니다.

### 🔍 인덱스 (Index)
책의 '색인'과 같습니다. `WHERE` 절 조회 속도를 높여주지만, `INSERT/UPDATE/DELETE` 성능은 저하됩니다 (인덱스도 갱신해야 하므로).
*   **Clustered Index**: 실제 데이터가 인덱스 순서대로 정렬됨 (테이블당 1개, 주로 PK). 빠름.
*   **Non-Clustered Index**: 별도의 인덱스 페이지를 생성하고 데이터 위치를 가리킴.

### 🔗 조인 (Join)
두 개 이상의 테이블을 결합하는 연산입니다.

```sql
-- Inner Join: 양쪽 모두에 존재하는 데이터만
SELECT * FROM Users A INNER JOIN Orders B ON A.id = B.user_id;

-- Left Outer Join: A 테이블 데이터는 모두 포함 + B 테이블 데이터 매칭
SELECT * FROM Users A LEFT JOIN Orders B ON A.id = B.user_id;
```

---

## 4. 트랜잭션 (Transaction)

데이터베이스의 상태를 변화시키는 작업의 논리적 단위입니다.

### 🛡️ ACID 성질 (필수 암기)
1.  **원자성 (Atomicity)**: All or Nothing. 모두 성공하거나, 모두 실패해야 한다. (중간에 멈춤 없음)
2.  **일관성 (Consistency)**: 트랜잭션 전후에 데이터베이스 제약 조건이 유지되어야 한다.
3.  **격리성 (Isolation)**: 여러 트랜잭션이 동시에 실행될 때 서로 영향을 주면 안 된다.
4.  **지속성 (Durability)**: 성공한 트랜잭션은 영구적으로 반영되어야 한다.

---

## 5. 데이터베이스 설계 (정규화)

데이터 중복을 줄이고 이상 현상(Anomaly: 삽입, 삭제, 갱신 이상)을 방지하기 위해 테이블을 쪼개는 과정입니다.

*   **제1정규형 (1NF)**: 모든 속성값은 원자값(Atomic Value)이어야 한다. (하나의 칸에 값 하나)
*   **제2정규형 (2NF)**: 부분 함수 종속 제거. (PK의 일부에만 종속되는 컬럼 분리)
*   **제3정규형 (3NF)**: 이행 함수 종속 제거. (A->B, B->C 일 때 A->C인 관계 분리)
*   **BCNF**: 모든 결정자가 후보키여야 함.
*   **역정규화 (De-normalization)**: 성능을 위해 의도적으로 중복을 허용하고 테이블을 합치는 것. (실무에서 조인 비용 줄이기 위해 자주 사용)

---

## 6. NoSQL 및 분산 처리

대용량 데이터를 처리하기 위한 현대적 아키텍처입니다.

*   **파티셔닝 (Partitioning)**: 큰 테이블을 물리적으로 여러 개로 나누는 것.
*   **샤딩 (Sharding)**: 데이터를 여러 대의 **서버**에 분산 저장하는 것. (Horizontal Partitioning)
*   **CAP 이론**: 분산 시스템에서 Consistency(일관성), Availability(가용성), Partition Tolerance(분할 허용) 세 가지를 모두 만족할 수는 없다. (보통 CP나 AP 선택)

---

## 🎓 Data Engineer & ML Interview Q&A

**Q1. 인덱스(Index)를 걸면 무조건 좋은가요? 사용 시 주의할 점은?**
> **A.** 조회 성능은 향상되지만, 데이터 변경(`INSERT`, `UPDATE`, `DELETE`) 시 인덱스도 함께 업데이트해야 하므로 쓰기 성능이 저하됩니다. 또한 인덱스 자체도 저장 공간을 차지합니다. 따라서, **조회 빈도가 높고 카디널리티(Cardinality, 중복도가 낮은)가 높은 컬럼**에 선별적으로 적용해야 합니다.

**Q2. 트랜잭션 격리 수준(Isolation Level)에 대해 설명해 주세요.**
> **A.** 동시에 여러 트랜잭션이 처리될 때 서로 얼마나 격리할지 결정하는 수준입니다.
> 1. `READ UNCOMMITTED`: 커밋되지 않은 데이터도 읽음 (Dirty Read 발생).
> 2. `READ COMMITTED`: 커밋된 데이터만 읽음 (가장 많이 사용).
> 3. `REPEATABLE READ`: 트랜잭션 내에서 동일한 조회 결과 보장 (MySQL 기본).
> 4. `SERIALIZABLE`: 완벽한 격리, 성능 가장 낮음.

**Q3. 정규화를 해야 하는 이유와 역정규화(De-normalization)를 하는 이유는?**
> **A.** 정규화는 중복 데이터를 제거하여 **용량을 줄이고 데이터 무결성을 유지(이상 현상 방지)**하기 위해 수행합니다. 하지만 테이블이 너무 많이 쪼개지면 **조인(Join) 연산이 많아져 조회 성능이 떨어질 수 있습니다**. 이럴 때 성능 향상을 위해 의도적으로 테이블을 합치는 역정규화를 수행합니다.

---

## 🔬 Deep Dive: DB 엔진의 심장부

### 1. 인덱스 내부 구조: B-Tree vs B+Tree
대부분의 현대 DBMS(Oracle, MySQL InnoDB 등)는 **B+Tree**를 사용합니다. 왜일까요?
*   **B-Tree**: 모든 노드가 데이터(Value)를 저장합니다. (파일 시스템 등에서 사용)
*   **B+Tree**: **리프 노드(Leaf Node)**에만 실제 데이터가 저장되고, 내부 노드(Internal Node)는 인덱스(Key) 역할만 합니다. 또한 리프 노드끼리 **연결 리스트(Linked List)**로 이어져 있습니다.
    *   **장점 1**: 한번에 더 많은 Key를 메모리에 올릴 수 있어(Fan-out이 큼) 트리의 높이가 낮아집니다. (Disk I/O 감소)
    *   **장점 2**: 리프 노드가 연결되어 있어 **범위 검색(Range Scan)**이 매우 빠릅니다. (풀스캔 유리)

### 2. 트랜잭션 격리 수준과 이상 현상 (Anomalies)
격리 수준이 낮을 때 발생하는 문제점들을 정확히 구분해야 합니다.
*   **Dirty Read**: 커밋되지 않은 데이터를 읽음 (`READ UNCOMMITTED`).
*   **Non-Repeatable Read**: 같은 트랜잭션 내에서 조회를 두 번 했는데 값이 달라짐 (다른 트랜잭션이 UPDATE/COMMIT함). (`READ COMMITTED`에서 발생)
*   **Phantom Read**: 같은 트랜잭션 내에서 조회를 두 번 했는데 없던 레코드가 생김 (다른 트랜잭션이 INSERT/COMMIT함). (`REPEATABLE READ`에서도 발생 가능하나, MySQL은 Gap Lock으로 방지)

### 3. MVCC (Multi-Version Concurrency Control)
"락(Lock)을 걸면 느려지는데, 락 없이 일관된 읽기를 할 수 없을까?"
*   **원리**: 데이터를 업데이트할 때 덮어쓰지 않고, **새로운 버전(Snapshot)**을 만듭니다. (Undo Log 활용)
*   **효과**: 읽기 작업은 락을 걸지 않고 특정 시점의 스냅샷을 읽으면 되므로, **읽기와 쓰기가 서로를 방해하지 않습니다**. (Reader-Writer Conflict 해결)

### 4. 분산 데이터베이스 이론
*   **Sharding Strategy**:
    *   **Hash Sharding**: `hash(key) % N`으로 서버 결정. 데이터가 고르게 분산되지만, 서버 추가/삭제 시 대규모 데이터 이동 필요 (Consistent Hashing으로 완화).
    *   **Range Sharding**: `Key` 범위에 따라 분산 (예: 날짜별, ID 구간별). 특정 범위에 트래픽이 몰리는 **Hotspot** 문제 발생 가능.
*   **PACELC 이론**: CAP 이론의 확장판. "네트워크 파티션(P) 상황이 아닐 때(E), 가용성(A)과 지연시간(L) 중 무엇을 희생할 것인가(C)?"를 고민해야 합니다.