## LlamaIndex Intro

### Source

- [AI 기반 SQL 분석 에이전트 구축 - 05. LlamaIndex Intro](https://siapapa.github.io/day1/05-llamaindex-intro/)

### 1. RAG(Retrieval-Augmented Generation) = 오픈북 시험

- LLM은 학습 데이터에 없는 정보를 모른다.
  - 회사 내부 데이터
  - 최신 정보
  - 그래서 없는 정보를 그럴듯하게 만들어내는 할루시네이션이 생길 수 있다

- RAG는 이런 한계를 보완하는 방식이다.
- 핵심 아이디어는 **관련 자료를 먼저 찾고(Retrieval), 그 자료를 LLM에 함께 넣어(Augmented), 답변을 생성(Generation)하게 하는 것**이다.

### 동작 과정 예시

질문이 `"내과에 어떤 의사가 있나요?"` 라고 들어오면:

1. **검색(Retrieval)**: 관련 문서를 찾는다.
2. **증강(Augmented)**: 찾은 문서와 질문을 함께 LLM에 전달한다.
3. **생성(Generation)**: LLM이 그 문맥을 바탕으로 답변한다.

즉, 흐름은 다음처럼 이해할 수 있다.

`질문 -> 관련 문서 검색 -> 질문 + 문서 컨텍스트 전달 -> LLM 답변 생성`

> 한 줄 정리: RAG는 AI에게 참고 자료를 건네준 뒤 답하게 만드는 "오픈북 시험" 방식이다.

### 2. LlamaIndex 5단계 파이프라인

LlamaIndex는 RAG를 다음 5단계로 다루도록 도와준다.

1. **Documents**
   - 원본 문서를 불러온다.
   - 예: PDF, CSV, SQL 문서

2. **Nodes (Chunks)**
   - 문서를 검색 가능한 작은 조각으로 나눈다.
   - 긴 문서를 그대로 넣지 않고, 검색 단위로 쪼개는 단계다.

3. **Embeddings**
   - 각 조각을 숫자 벡터로 변환한다.
   - 의미가 비슷한 텍스트끼리 가까워지도록 표현한다.

4. **Index**
   - 벡터를 저장하고 검색 가능한 구조로 만든다.
   - 보통 벡터 DB와 연결되는 단계다.

5. **Query Engine**
   - 질문을 받아 검색하고, 검색 결과를 바탕으로 최종 답변까지 만든다.

흐름으로 보면:

`Documents -> Nodes -> Embeddings -> Index -> Query Engine`

> 핵심 포인트: 강의 전반에서 반복되는 구조는 결국 "문서를 잘게 자르고, 벡터로 바꾸고, 저장하고, 꺼내 써서 답하게 만드는 흐름"이다.

### 3. Query Engine vs Retriever

- **Query Engine**은 `검색 + LLM 답변 생성`을 한 번에 수행한다.
- **Retriever**는 `검색만` 수행한다.

역할 차이는 다음처럼 보면 쉽다.

- **Query Engine** = 최종 사용자용
- **Retriever** = 디버깅/분석용

왜 둘을 나눠 보느냐가 중요하다.

- RAG 답변이 이상할 때 원인이 두 가지일 수 있다.
  - 아예 엉뚱한 문서를 검색했다
  - 문서는 맞았는데 LLM이 답변을 잘못 만들었다

그래서 실무에서는 보통 이 순서가 좋다.

1. **Retriever**로 먼저 올바른 문서가 검색되는지 확인한다.
2. 그다음 **Query Engine**으로 최종 답변 품질을 검증한다.

> 한 줄 정리: 검색이 맞는지 먼저 보고, 그다음 답변이 좋은지 본다. 이것이 RAG 디버깅의 기본 순서다.
