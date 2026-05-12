## LangChain LCEL

### Source

- [AI 기반 SQL 분석 에이전트 구축 - 15. LangChain LCEL](https://siapapa.github.io/day3/15-langchain-lcel/)

### 1. LCEL 개념 -- "레고 블록 조립"

- LCEL은 LangChain Expression Language의 약자다.
- 핵심 아이디어는 체인을 거대한 한 덩어리로 짜는 대신, **작은 블록을 조립하듯 연결하는 것**이다.

왜 "레고 블록 조립"인가:

- 프롬프트 블록
- 모델 블록
- 파서 블록
- 전처리/후처리 블록

이런 조각들을 이어 붙여 원하는 파이프라인을 만든다.

장점은 명확하다.

- 흐름이 잘 보인다
- 부분 교체가 쉽다
- 디버깅이 쉽다
- 재사용이 쉽다

> 한 줄 정리: LCEL은 LLM 체인을 "큰 프로그램"이 아니라 "조립 가능한 블록 묶음"으로 다루게 해 준다.

### 2. RunnablePassthrough, RunnableLambda, RunnableParallel

이 세 가지는 LCEL에서 데이터 흐름을 제어할 때 자주 쓰는 기본 유틸리티다.

#### RunnablePassthrough

- 입력을 **그대로 전달**한다.
- 필요한 곳에 원래 입력값을 그대로 넘기고 싶을 때 쓴다.

예:

- `{"question": RunnablePassthrough()}`

주의:

- 딕셔너리 입력이 필요한 경우, 그냥 단독으로 쓰지 말고 키와 함께 감싸는 형태가 자주 필요하다.

#### RunnableLambda

- 파이썬 함수를 체인 안에 넣는 방식이다.
- 입력을 조금 가공하거나 변환할 때 유용하다.

예:

- 대문자로 바꾸기
- 특정 필드만 추출하기
- 문자열 전처리하기

#### RunnableParallel

- 여러 작업을 **동시에 실행**한다.
- 예를 들어 같은 질문에 대해
  - SQL 생성
  - 자연어 요약
를 병렬로 돌릴 수 있다.

> 외우는 법: `Passthrough = 통과`, `Lambda = 변환`, `Parallel = 동시에`.

### 3. 구조화 출력 -- with_structured_output (Pydantic)

- 구조화 출력은 AI 답변을 자유 텍스트가 아니라 **정해진 필드 구조**로 받는 방식이다.
- 예를 들어
  - `tables`
  - `sql`
  - `difficulty`
처럼 미리 정한 양식으로 답을 받게 만들 수 있다.

강의 핵심:

- `Pydantic` 스키마를 정의하고
- `model.with_structured_output(Schema)` 를 사용하면
- LLM이 그 스키마에 맞는 결과를 반환하도록 유도할 수 있다

왜 중요한가:

- 결과를 문자열로 후처리하지 않아도 된다
- 필드 단위로 바로 접근할 수 있다
- 에이전트나 파이프라인에서 다음 단계로 넘기기 쉽다

예를 들면 반환값을 이렇게 다룰 수 있다.

- `result.tables`
- `result.sql`
- `result.difficulty`

강의 표현대로 보면, `Pydantic`과 구조화 출력은 결국:

> **"AI에게 양식을 채우게 시키는 도구"**

라고 이해하면 된다.

### 한 줄 정리

- LCEL은 체인을 블록처럼 조립하게 해 주고, `Runnable*`은 그 흐름을 제어하며, `with_structured_output`은 결과를 코드가 바로 쓰기 좋은 구조로 바꿔준다.
