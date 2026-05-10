## RDB And SQL

### Topic Map

- `01AgenticAnalyticsOverview.md`: 데이터 분석의 3세대, 왜 에이전트인가, 에이전트의 4가지 핵심 요소
- `02PostgreSQLBasics.md`: 왜 PostgreSQL인가, DDL 제약조건, SELECT 기본 문법, EXPLAIN 맛보기
- `03SQLAdvanced.md`: GROUP BY, JOIN, 서브쿼리, CTE, 윈도우 함수
- `04SchemaIntelligence.md`: AI가 읽기 좋은 스키마, 좋은 네이밍과 설계 원칙
- `05LlamaIndexIntro.md`: RAG 개념, LlamaIndex 파이프라인, Query Engine과 Retriever
- `06EmbeddingAndVectorBasics.md`: 임베딩, 코사인 유사도, 모델 비교, t-SNE
- `07TextToSQLIntro.md`: Text-to-SQL 개념, 생성 흐름, 실패 원인, 보안 기초
- `08TextToSQLImprovementStrategies.md`: Text-to-SQL 정확도 개선 전략 3가지
- `09MultiTurnChatbotAndSQLGuardrails.md`: 멀티턴 상태 관리와 SQL 보안 가드레일
- `10GradioUI.md`: Gradio 선택 이유, Drive 저장, Hugging Face Spaces 배포

### Quick Summary

1. 데이터 분석은 BI 대시보드에서 Text-to-SQL, 그리고 Agentic Analytics로 발전하고 있다.
2. 에이전트는 한 번 생성하고 끝내는 것이 아니라 계획, 실행, 검증, 재시도를 반복한다.
3. 에이전트의 핵심 요소는 상태, 도구, 계획, 검증이다.
4. PostgreSQL은 AI 가독성과 SQL 학습 친화성 때문에 좋은 출발점이다.
5. 고급 SQL은 집계, 결합, 단계화, 행 단위 비교를 다루는 도구들로 확장된다.
6. AI 정확도를 높이려면 스키마 자체를 사람이 아니라 AI도 읽기 쉽게 설계해야 한다.
7. RAG 시스템은 검색 품질과 최종 답변 품질을 분리해서 점검하는 습관이 중요하다.
8. 벡터 검색을 이해하려면 임베딩과 코사인 유사도 개념이 먼저 잡혀야 한다.
9. Text-to-SQL의 정확도와 안전성은 질문의 명확성, 스키마 품질, 권한 통제에 크게 좌우된다.
10. Text-to-SQL 품질은 스키마 보강, 예시 주입, 관련 테이블 축소로 크게 개선할 수 있다.
11. 멀티턴 챗봇은 상태 관리가 핵심이고, SQL 보안은 정규식만으로 끝나지 않는다.
12. 학습용 AI 데모는 Gradio로 빠르게 만들고, 영구 배포는 별도 플랫폼으로 넘기는 흐름이 실용적이다.
