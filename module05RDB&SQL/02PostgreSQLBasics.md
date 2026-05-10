## PostgreSQL Basics

### Source

- [AI 기반 SQL 분석 에이전트 구축 - 02. PostgreSQL Basics](https://siapapa.github.io/day1/02-postgres-basics/)

### 왜 PostgreSQL인가?

| 특성 | PostgreSQL | 메모 |
| --- | --- | --- |
| SQL 표준 준수 | 높음 | 정석적인 SQL 학습에 유리 |
| `COMMENT ON` 지원 | 가능 | AI가 스키마를 읽기 쉬움 |
| 윈도우 함수 | 완전 지원 | 분석 SQL 확장에 유리 |

- PostgreSQL은 SQL 표준 준수도가 높아서 학습용과 실무용 모두에 적합하다.
- 분석 SQL에서 자주 쓰는 기능을 폭넓게 지원한다.
- 특히 **AI 가독성** 측면이 중요하다.

> **핵심 이유:** `COMMENT ON`으로 테이블/컬럼에 설명을 달 수 있어서 AI가 스키마를 이해하기 쉽다. 이것이 PostgreSQL을 선택한 핵심 이유다.

### DDL 제약조건 치트시트

강의 스키마에서 계속 등장한 키워드 5가지는 아래와 같다.

| 키워드 | 의미 | 예시 | 안 쓰면? |
| --- | --- | --- | --- |
| `SERIAL` | 자동 증가 정수 컬럼의 간단한 표현 | `doctor_id SERIAL PRIMARY KEY` | ID를 직접 넣어야 함 |
| `PRIMARY KEY` | 각 행을 고유하게 식별 | `PRIMARY KEY (doctor_id)` | 중복과 식별 문제 발생 |
| `REFERENCES` | 다른 테이블의 존재하는 값만 허용 | `department_id INT REFERENCES departments(department_id)` | 고아 데이터가 생길 수 있음 |
| `NOT NULL` | 빈 값 금지 | `name VARCHAR(100) NOT NULL` | 필수 정보 누락 가능 |
| `CHECK (...)` | 값의 허용 범위를 제한 | `CHECK (gender IN ('M','F'))` | 쓰레기 값 유입 가능 |

- 강의에서는 학습 편의를 위해 `SERIAL`을 사용했지만, 실무에서는 `GENERATED ... AS IDENTITY`도 많이 쓴다.
- `REFERENCES`, `NOT NULL`, `CHECK`는 데이터 품질을 지키는 최소 장치다.

### SELECT 기본 문법 — 데이터 조회

처음 배울 때는 아래 4개를 중심으로 익히면 된다.

1. **`SELECT`**: 어떤 열을 볼지 고른다.
2. **`WHERE`**: 조건으로 행을 필터링한다.
3. **`ORDER BY`**: 결과를 정렬한다.
4. **`LIMIT`**: 상위 N개만 본다.

강의 예시는 다음 흐름으로 구성된다.

- `SELECT * FROM patients LIMIT 5`
  - 테이블 미리보기

- `SELECT patient_id, name, gender, blood_type FROM patients LIMIT 10`
  - 원하는 열만 선택

- `SELECT ... FROM patients WHERE gender = 'F' ORDER BY birth_date`
  - 조건 필터링 + 정렬

- `SELECT ... FROM visits v JOIN patients p ... ORDER BY v.cost DESC LIMIT 5`
  - 조인 + 정렬 + 상위 N개

> 한 줄 정리: `SELECT`는 조회, `WHERE`는 필터, `ORDER BY`는 정렬, `LIMIT`는 상위 N개 보기다.

### EXPLAIN 맛보기

- `EXPLAIN`은 SQL이 **어떻게 실행되는지** 보는 도구다.
- 지금 단계에서는 실행 계획의 세부 항목을 다 이해할 필요는 없다.
- 우선은 "이 SQL이 빠를지 느릴지 확인하는 성능 분석 도구" 정도로 기억하면 충분하다.

강의 예시처럼 다음 형태로 자주 사용한다.

```sql
EXPLAIN (FORMAT TEXT)
SELECT p.name, v.visit_date
FROM visits v
JOIN patients p ON p.patient_id = v.patient_id
WHERE v.visit_date >= '2026-01-01';
```

- 결과를 보고 어떤 테이블을 먼저 읽는지,
- 조인이 어떻게 일어나는지,
- 전체 실행 흐름이 어떤지 감을 잡는 것이 첫 단계다.

### 한 줄 정리

- PostgreSQL 입문에서 중요한 포인트는 **스키마를 정확히 만들고, `SELECT`로 읽고, `EXPLAIN`으로 실행 방식을 보는 습관**이다.
