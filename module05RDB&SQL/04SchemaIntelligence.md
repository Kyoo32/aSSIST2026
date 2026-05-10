## Schema Intelligence

### Source

- [AI 기반 SQL 분석 에이전트 구축 - 04H. Schema Intelligence](https://siapapa.github.io/day1/04-schema-intelligence/)

### 1. AI는 스키마를 "텍스트"로 읽는다

- Text-to-SQL 시스템에서 LLM은 데이터베이스 스키마를 **프롬프트의 일부 텍스트**로 받는다.
- 즉, 사람 눈에만 익숙한 축약형 컬럼명은 AI에게는 불친절한 암호처럼 보일 수 있다.

나쁜 스키마에서는 AI가 계속 추측해야 한다.

- `p`는 `patients`인지 `products`인지
- `nm`은 `name`인지
- `gen`은 `gender`인지 `generation`인지
- `bt`는 `blood_type`인지 `batch`인지

좋은 스키마에서는 이런 추측이 거의 필요 없다.

```sql
CREATE TABLE patients (
    patient_id   SERIAL PRIMARY KEY,
    name         VARCHAR(100) NOT NULL,
    gender       CHAR(1) NOT NULL CHECK (gender IN ('M','F')),
    birth_date   DATE NOT NULL,
    blood_type   VARCHAR(3) CHECK (blood_type IN ('A','B','O','AB'))
);

COMMENT ON TABLE patients IS '환자 기본 정보';
COMMENT ON COLUMN patients.gender IS '성별: M=남성, F=여성';
COMMENT ON COLUMN patients.blood_type IS '혈액형: A, B, O, AB';
```

> 핵심 포인트: AI는 스키마를 코드 구조가 아니라 텍스트 설명처럼 읽기 때문에, **명시적 이름 + COMMENT ON** 이 SQL 정확도를 크게 좌우한다.

### 좋은 스키마 — AI가 즉시 이해

- 좋은 스키마의 목표는 "AI가 추측할 것 0개"에 가깝게 만드는 것이다.
- 이름만 보고 의미를 알 수 있고,
- 제약조건만 봐도 값의 범위를 이해할 수 있으며,
- `COMMENT ON`으로 도메인 의미까지 전달할 수 있어야 한다.

즉, 좋은 스키마는 단순히 DB를 저장하기 위한 구조가 아니라, **AI가 바로 SQL을 생성할 수 있는 설명서** 역할도 한다.

### 2. 5가지 설계 원칙

1. **명시적 네이밍**
   - `p_id`, `nm`, `gen`보다 `patient_id`, `name`, `gender`처럼 바로 이해되는 이름을 쓴다.
   - 축약보다 의미가 우선이다.

2. **COMMENT ON**
   - 테이블과 컬럼에 자연어 설명을 붙인다.
   - 이 설명은 LLM 프롬프트에 포함되어 SQL 생성 정확도를 높인다.

3. **FK 명시**
   - `patient_id INT REFERENCES patients`처럼 참조 관계를 분명히 적는다.
   - 관계를 명시해야 AI도 테이블 연결 방식을 쉽게 이해한다.

4. **ENUM -> 룩업 테이블 고려**
   - 단순 `CHECK (status IN (...))`를 넘어서, 상태값이 많아지면 별도 룩업 테이블로 분리하는 것이 더 명확할 수 있다.
   - 코드값의 의미를 관리하기 쉬워진다.

5. **리포팅 뷰 제공**
   - 매번 여러 단계 JOIN이 필요한 구조라면, 자주 쓰는 결합 결과를 뷰로 미리 제공할 수 있다.
   - 예: `vw_visit_details`

### 실전 감각으로 기억하기

- AI 친화적 스키마는 결국 다음 질문에 답할 수 있어야 한다.
  - 테이블 이름만 보고 무슨 데이터인지 알 수 있는가?
  - 컬럼 이름만 보고 의미를 알 수 있는가?
  - 관계가 FK로 드러나는가?
  - 코드값 의미가 주석이나 구조로 설명되는가?
  - 자주 쓰는 분석 경로가 뷰로 정리되어 있는가?

### 한 줄 정리

- 스키마 설계는 저장 구조를 만드는 작업이면서 동시에, **AI가 오해 없이 SQL을 만들 수 있게 문맥을 심어두는 작업**이다.
