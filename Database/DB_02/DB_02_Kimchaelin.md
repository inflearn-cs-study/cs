# 데이터베이스 키(Key)의 종류와 무결성 제약 조건
## 데이터베이스 키(Key)의 종류
### 1. 기본키(Primary Key)
- 테이블에서 각 행을 **유일하게 식별**할 수 있는 키.
- **유일성**과 **최소성**을 만족.
- NULL 값과 중복 불가.

### 2. 후보키(Candidate Key)
- 테이블에서 기본키의 후보가 되는 키.
- **유일성**과 **최소성**을 만족.
- NULL 값과 중복 불가.

### 3. 대체키(Alternate Key)
- 후보키 중 기본키로 선정되지 않은 나머지 키.
- **유일성**은 만족하지만 NULL 값 가능.

### 4. 슈퍼키(Super Key)
- 테이블에서 **유일성**을 만족하는 키 집합.
- **최소성**을 만족하지 않을 수 있음.
- 기본키, 후보키, 대체키의 조합으로 이루어짐.
- NULL 값 가능.

### 5. 외래키(Foreign Key)
- 다른 테이블의 기본키를 참조하는 키.
- 두 테이블을 연결하기 위해 사용.

### 6. 복합키(Composite Key)
- 두 개 이상의 속성을 조합하여 만든 키.
- **유일성**을 만족.

### 7. 유니크 키(Unique Key)
- 중복을 허용하지 않는 키.
- 기본키와 유사하지만 NULL 값이 **하나만 허용**됨.

> 유일성 : 테이블 내에서 동일한 값이 존재하지 않음.
> 
>최소성 : 최소한의 속성으로 유일성을 보장.

---

## 데이터베이스 무결성 제약 조건
**무결성**은 데이터의 **정확성**과 **일관성**을 보장하기 위한 제약 조건입니다.

### 1. 개체 무결성(Entity Integrity)
- 각 행은 고유해야 함.
- 기본키는 NULL이거나 중복되지 않아야 함.

### 2. 참조 무결성(Referential Integrity)
- 외래키 값은 NULL이거나 참조하는 테이블의 기본키 값이어야 함.
- 참조 무결성을 위반하면 연결된 테이블의 데이터를 조작할 수 없음.

### 3. 도메인 무결성(Domain Integrity)
- 속성의 값은 정의된 **도메인**(데이터 타입, 값의 범위 등)에 속해야 함.
- 데이터 타입, NULL 허용 여부, 범위 등을 제약.

### 4. 고유 무결성(Unique Integrity)
- 릴레이션의 특정 속성에 대해 각 튜플이 갖는 속성값들이 서로 달라야 함.

### 5. 키 무결성(Key Integrity)
- 하나의 릴레이션에는 적어도 하나의 키가 존재해야 함.

### 6. 사용자 정의 무결성(User-Defined Integrity)
- 사용자가 정의한 무결성 규칙.

---

# MySQL과 InnoDB의 주요 특징 및 동작 원리

## MySQL
**MySQL**은 관계형 데이터베이스 관리 시스템(RDBMS) 중 하나입니다.

### 구조
![MySQL 구조](https://velog.velcdn.com/images/juhyeon1114/post/481e372e-ce63-40f9-a3bb-eae59e36fd33/image.jpg)

- **커넥션 풀**: 미리 커넥션을 생성하고 요청이 들어오면 제공.
- **MySQL 엔진**: SQL문을 처리하고, 데이터를 읽고 쓰는 역할.
- **스토리지 엔진**: 데이터를 저장하고 관리.

### 주요 특징
- 오픈 소스이며 다양한 운영체제 지원.
- 다중 사용자와 다중 스레드 지원.

---

## InnoDB
**InnoDB**는 MySQL과 연동 가능한 플러그인 형태의 스토리지 엔진 중 하나입니다.

### 구조
![InnoDB 구조](https://velog.velcdn.com/images/ddangle/post/49a6c413-42d8-4202-9ca4-f3589cad438e/image.png)

- **메모리 영역**: 버퍼 풀 등 데이터 캐싱.
- **CPU 연산 영역**: 데이터 처리 및 연산.
- **디스크 영역**: 실제 데이터를 저장.

### 주요 특징
1. **외래 키 지원**
    - 테이블 간 관계를 유지하며 참조 무결성을 보장.

2. **트랜잭션 지원**
    - **ACID** 특성을 만족하여 데이터 무결성을 보장.

3. **클러스터링 (Clustered Index)**
    - 기본키로 데이터가 정렬되어 있어, 검색 속도가 빠름.

4. **MVCC 방식 사용**
    - **MVCC (Multi-Version Concurrency Control)**:
        - 동시 작업을 처리하고 트랜잭션 간 충돌을 방지.
        - 쓰기 작업 시 기존 레코드를 복사하여 새로운 버전을 생성.
        - 읽기 작업 시 이전 버전을 제공.

5. **자동 데드락 감지**
    - 교착 상태 발생 시 이를 자동으로 감지하고 해결.

6. **버퍼 풀 (Buffer Pool)**
    - 디스크에서 데이터를 읽지 않고, 메모리에 데이터를 캐싱하여 빠른 읽기/쓰기 제공.
