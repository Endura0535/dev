---
description: EXPLAIN 구문, SELECT TYPE, JOIN TYPE, EXTRA TYPE
---

# DB 개선 ② - 실행 계획

## EXPLAIN 구문

<mark style="background-color:blue;">SQL 쿼리의 실행 계획</mark>을 보여주는 명령어

사용법

```sql
EXPLAIN SELECT * FROM employees WHERE emp_no = 10001;
```

## SELECT TYPE

| 종류                       | 설명                             |
| ------------------------ | ------------------------------ |
| **SIMPLE**               | 서브쿼리나 UNION이 없는 단일 SELECT      |
| **PRIMARY**              | 가장 바깥쪽 SELECT (최상위)            |
| **SUBQUERY**             | WHERE나 SELECT 절 안의 서브쿼리        |
| **DERIVED**              | FROM 절 내부의 서브쿼리 (파생 테이블)       |
| **UNION**                | UNION의 두 번째 이후 SELECT          |
| **UNION RESULT**         | UNION 결과를 결합하는 내부 SELECT       |
| **DEPENDENT SUBQUERY**   | 외부 쿼리 컬럼을 참조하는 서브쿼리            |
| **DEPENDENT DERIVED**    | 외부 쿼리를 참조하는 파생 테이블             |
| **MATERIALIZED**         | 파생 테이블을 메모리에 저장해 재사용           |
| **UNCACHEABLE SUBQUERY** | 결과를 캐시할 수 없는 서브쿼리 (ex. 랜덤값 포함) |

🚨 `UNION`, `UNION RESULT`  **→** 성능상 좋지 않아 튜닝 대상

## JOIN TYPE

| 종류          | 설명                                      | 성능      |
| ----------- | --------------------------------------- | ------- |
| **system**  | row가 1개뿐인 테이블                           | ✅ 최고    |
| **const**   | PK 또는 UNIQUE로 row 1개만 조회                | ✅ 매우 좋음 |
| **eq\_ref** | 조인에서 정확히 1개의 매칭 row (UNIQUE + NOT NULL) | ✅ 매우 좋음 |
| **ref**     | 조인 시 여러 행 매칭 (외래 키 등)                   | ✅ 좋음    |
| **range**   | 인덱스 범위 조회 (BETWEEN, > 등)                | ✅ 괜찮음   |
| **index**   | 인덱스 전체 스캔 (테이블 접근은 없음)                  | ⚠️ 중간   |
| **ALL**     | 테이블 전체 스캔 (Full Table Scan)             | ❌ 성능 나쁨 |

🚨 `ALL`은 **가장 비효율적 →** 인덱스를 고려하거나 쿼리 리팩토링이 필요

**✔ `JOIN`이 많을수록** `type` 확인이 중요

**✔** `EXPLAIN` 결과의 순서를 따라 조인 계획을 파악 가능

## EXTRA TYPE

| 종류                           | 설명                         | 성능 영향         |
| ---------------------------- | -------------------------- | ------------- |
| **Using where**              | WHERE 조건으로 row 필터링         | ⚠️ 조건 연산 필요   |
| **Using index**              | 인덱스만으로 처리 (커버링 인덱스)        | ✅ 매우 효율적      |
| **Using where; Using index** | 인덱스 사용 + 조건 필터링            | ✅ 좋음          |
| **Using temporary**          | 임시 테이블 사용 (GROUP BY 등)     | ❌ 성능 저하 가능    |
| **Using filesort**           | 정렬용 임시 정렬 알고리즘 사용          | ❌ 느림          |
| **Using join buffer**        | 인덱스 없이 조인 버퍼 사용            | ❌ 비효율적 조인     |
| **Impossible WHERE**         | WHERE 조건이 항상 false         | ✅ 빠름 (결과 없음)  |
| **Distinct**                 | 중복 제거 수행 중                 | ⚠️ 데이터 크기에 영향 |
| **FirstMatch(tbl)**          | 첫 번째 매칭만 사용 (세미조인 최적화)     | ✅             |
| **LooseScan**                | Index Loose Scan 최적화 방식 사용 | ✅             |

✔ `Using index` 가 성능이 좋음



> 📚 참고: 『개발자 기술 면접 노트』 – 이남희 지음
