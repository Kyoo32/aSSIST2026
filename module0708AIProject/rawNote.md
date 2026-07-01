## Raw Note

### 개론: 역사와 발전

- `Perception -> Generative -> Agentic -> Physical`
- `LLM -> RAG -> Agentic AI`
- `Prompt Engineering -> Context Engineering -> Harness`
  - RAG도 Prompt/Context Engineering의 일종
  - `VectorDB + RQLKey + TF-IDF = Hybrid RAG`
  - Re-Rank 등등 = Advanced RAG
  - Agentic RAG

### LLM Tuning

- 거대모델 -> 아키텍쳐 -> 파인튜닝/정렬 -> 추론 -> 압축/서빙
  - 파인튜닝: `SFT -> RLHF -> DPO/GRPO`
  - 모델 자체 바꾸기
  - 추론: 모델 가중치는 그대로 두고 입력/출력/탐색 방식을 조작
  - 압축&서빙: 메모리 줄이고 프로덕션 환경에서 트래픽 처리
  - Edge / Mobile

### Thinking Process

- Test-Time Scaling
  - 추론 엔진 중심 + 외부 도구 시스템으로 분리
  - 프롬프트 아키텍쳐 -> SSD & Clean 아키텍쳐
- 메모리 사용량 폭증
  - KeyValue 캐시 누적
  - hidden tokens 대량 사용
- Short-term memory: `HBM Local`
- Long-term memory: `SSD`, `NAND`

### Agentic AI

- `A2A protocol`
- 아키텍쳐 구조
  - 1. 인지
  - 2. 지식 & 메모리
  - 3. 제어 & 실행: AgenticRAG -> SDD
  - 4. 검증

### 검색

- key: `RDB`
- 의미: `VectorDB`
- 관계성: `Ontology / GraphDB`

### 기술 분류 공학 관점

- **AI Engineering**
  - 전통적인 모델링
  - LLM 이후 경제적·기능적 가치 없음
  - 학습은 튜닝이 트렌드: `LoRA`, `QLoRA`
  - 추론 경량화도 있음: `vLLM` (ex. KV Cache)
  - 전이학습?

- **AI Software**
  - `RAG`: hybridRAG, graphRAG
  - `agent`: 루브릭 평가 등 필요, 실패했을 때 처리 필요

- **AI Native**
  - AI와 코딩하기

### Multimodal

- merger로 데이터 종류 통합
- merger도 학습 필요
  - 대조학습
  - 정렬학습
