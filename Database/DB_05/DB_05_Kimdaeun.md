# 인덱스와 실행 계획

## **1. 인덱스의 개념과 설정 기준**
### **인덱스란?**
- 인덱스는 데이터베이스 테이블에서 검색 속도를 향상시키기 위해 사용하는 데이터 구조
- 책의 목차처럼 특정 열(column)의 값과 해당 행(row)을 빠르게 찾아갈 수 있도록 설계되어 있다.

### **인덱스의 주요 특징**
1. **검색 속도 향상**: 테이블의 전체 데이터를 스캔하는 대신, 인덱스를 활용해 원하는 데이터를 빠르게 찾을 수 있음.
2. **추가적인 저장 공간 사용**: 인덱스는 별도의 데이터 구조로 저장되므로 추가적인 디스크 공간을 차지.
3. **쓰기 성능 저하**: 데이터 삽입, 수정, 삭제 시 인덱스를 업데이트해야 하므로 성능에 영향을 미칠 수 있음.

---

### **인덱스 설정 기준**
1. **자주 조회되는 컬럼**
   - WHERE, JOIN, ORDER BY, GROUP BY 조건에서 자주 사용되는 컬럼에 인덱스를 설정.
   - 예:
     ```sql
     CREATE INDEX idx_employee_name ON employees(name);
     ```
2. **중복도가 낮은 컬럼**
   - 데이터가 고유하거나 중복도가 낮은 경우 인덱스 효과가 높음.
   - 예: 주민등록번호, 이메일 등.
3. **결과 데이터가 적은 경우**
   - 인덱스는 조회 대상 데이터가 전체의 일부일 때 성능 개선에 유리함.
   - 조회 대상이 전체 데이터의 대부분이라면 인덱스 효과가 떨어짐.
4. **복합 인덱스 (다중 컬럼 인덱스)**
   - 여러 컬럼을 함께 사용하는 경우 복합 인덱스를 설정.
   - WHERE 절에서 여러 컬럼을 조건으로 사용하는 경우 성능 개선 가능.
   - 예:
     ```sql
     CREATE INDEX idx_order_customer ON orders(order_date, customer_id);
     ```
5. **과도한 인덱스 설정 방지**
   - 너무 많은 인덱스는 쓰기 성능을 저하시킴.
   - 실제 쿼리 패턴에 맞는 인덱스만 설정.

---

### **다중 컬럼 인덱스의 동작**
- 다중 컬럼 인덱스는 지정된 컬럼 순서대로 인덱스가 생성됨.
- WHERE 조건에서 컬럼의 **순서를 고려**해야 인덱스를 제대로 활용 가능.

  ```sql
  CREATE INDEX idx_example ON table_name(col1, col2);
  ```
WHERE col1 = 'value1' 조건이 있을 때만 col2 인덱스가 효과적으로 작동한다.

---
## 2. 실행 계획(EXPLAIN)과 쿼리 힌트의 역할과 사용 방법

### 실행 계획(EXPLAIN)이란?
- EXPLAIN은 SQL 쿼리가 실행되는 과정을 보여주는 도구로, 데이터베이스가 쿼리를 처리하는 방식을 이해하고 최적화할 수 있도록 도움.
#### 1. EXPLAIN에서 제공하는 정보
- 쿼리에서 읽는 테이블 순서
- 인덱스 사용 여부 및 종류
- 조회된 데이터 양(행 수)
- 조인 순서 및 방법

#### 2.	결과 해석 주요 컬럼
- id: 쿼리 단계의 식별자.
- select_type: SELECT 유형 (단일, 서브쿼리, UNION 등).
- table: 데이터가 조회된 테이블.
- type: 조회 방식 (ALL, index, range 등).
- ALL: 테이블 전체 스캔(비효율적).
- index: 인덱스를 사용한 스캔.
- range: 범위 조건으로 데이터 검색.
- key: 사용된 인덱스.
- rows: 읽어야 할 데이터 행 수(작을수록 좋음).
- extra: 추가 정보 (Using index, Using temporary 등).

### 쿼리 힌트란?
- 쿼리 힌트는 데이터베이스에 특정 쿼리 실행 방식을 명시적으로 지시하는 방법
- 데이터베이스가 실행 계획을 생성하는 데 참고하도록 제공되며, 기본 계획보다 효율적인 실행을 유도

#### **1) 특정 인덱스 사용**
```sql
SELECT * FROM employees FORCE INDEX (idx_employee_name)
WHERE name = 'Alice';
```
- FORCE INDEX: 지정된 인덱스를 강제로 사용.
- USE INDEX: 지정된 인덱스를 우선적으로 사용.
- IGNORE INDEX: 특정 인덱스 사용을 무시.
#### 2) 조인 순서 제어
```sql
SELECT /*+ JOIN_ORDER(employees, departments) */ 
e.name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id;
```
- 조인 순서를 명시적으로 설정
  
