## AI Evolution And Project Landscape

### 1. AI 발전 흐름

메모의 가장 큰 줄기는 AI의 발전 단계를 프로젝트 관점으로 다시 묶는 것이다.

- **Perception**
- **Generative**
- **Agentic**
- **Physical**

이 흐름은 단순 모델 발전사가 아니라, AI 시스템이 점점 더 **행동하고 실행하는 방향**으로 이동하고 있다는 뜻이다.

### 2. LLM에서 Agentic AI로

메모는 기술 축도 단계적으로 정리한다.

- **LLM**
- **RAG**
- **Agentic AI**

한 줄 감각은 이렇다.

- LLM은 생성의 출발점
- RAG는 외부 지식을 붙이는 단계
- Agentic AI는 도구와 실행 흐름까지 붙이는 단계

### 3. Prompt Engineering에서 Context Engineering으로

메모는 다음 흐름을 강조한다.

- **Prompt Engineering**
- **Context Engineering**
- **Harness**

여기서 중요한 포인트는:

- RAG도 넓게 보면 Prompt/Context Engineering의 일부다
- 시스템 품질은 모델 하나보다도 **문맥을 어떻게 구성하고 운영하는지**에 좌우된다

### 4. RAG의 프로젝트 관점

메모에 나온 RAG 관련 키워드를 프로젝트 언어로 정리하면 이렇다.

- `VectorDB + RQLKey + TF-IDF = Hybrid RAG`
- Re-rank 등은 `Advanced RAG`
- 더 나아가면 `Agentic RAG`

즉, RAG도 단일 기법이 아니라:

- 검색 조합
- 문맥 구성
- 후처리
- 에이전트화

로 점점 확장된다.

### 5. LLM Tuning 전체 지도

메모는 튜닝을 모델 수명주기 관점으로 정리한다.

- 거대모델
- 아키텍처
- 파인튜닝/정렬
- 추론
- 압축/서빙

세부적으로 보면:

- **파인튜닝**
  - `SFT -> RLHF -> DPO / GRPO`
  - 모델 자체를 바꾸는 단계

- **추론**
  - 모델 가중치는 그대로 두고
  - 입력, 출력, 탐색 방식을 조정하는 단계

- **압축 / 서빙**
  - 메모리를 줄이고
  - 실제 프로덕션 트래픽을 처리하는 단계

추가 키워드:

- Edge
- Mobile

즉, 실전 프로젝트에서는 "모델을 잘 만드는 것"만이 아니라 "어떻게 돌릴 것인가"도 같은 비중으로 중요하다.

### 한 줄 정리

- 이 수업의 프로젝트 관점은 LLM 하나를 보는 것이 아니라, RAG와 Agentic AI까지 포함한 전체 AI 시스템 진화를 보는 데 있다.
