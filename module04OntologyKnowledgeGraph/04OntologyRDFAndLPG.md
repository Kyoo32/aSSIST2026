## Ontology, RDF, And LPG

### What Is Ontology

- 온톨로지는 세상의 개념과 관계를 정의하는 **의미 모델**이다.
- 단순 데이터 스키마를 넘어, "무엇이 어떤 개념이며 서로 어떻게 연결되는가"를 명시한다.

### RDF-Oriented Ontology

- RDF 계열에서는 schema가 중요한 역할을 한다.
- 주로 다음 요소를 중심으로 의미를 정의한다.
  - **Class**
  - **Property**
  - **Hierarchy**
  - **Binary relation**
  - **Instance of**

- 즉, 어떤 객체가 어떤 클래스에 속하고, 어떤 속성과 관계를 가지는지를 명시적으로 표현한다.

### LPG (Labeled Property Graph)

- LPG는 **Labeled Property Graph**의 약자다.
- RDF처럼 강하게 표준화된 온톨로지라기보다, 실용적으로 확장된 그래프 데이터 구조에 가깝다.
- 메모 관점에서는 **암묵적(implicit) 온톨로지**에 가깝다고 볼 수 있다.

### LPG Structure

- **노드(Node)**: 사람, 상품, 계좌 같은 객체 정보
- **관계(Edge)**: 구매, 친구, 소유 같은 연결 정보
- **속성(Property)**: 이름, 금액, 날짜 같은 세부 정보

### RDF Vs LPG

| 구분 | RDF 계열 | LPG |
| --- | --- | --- |
| 중심 관점 | 표준화된 의미 표현 | 실용적 그래프 활용 |
| 구조 | Triple 기반 | Node-Edge-Property 기반 |
| 강점 | 명시적 의미 정의 | 구현과 확장 편의성 |

### Practical Takeaway

- RDF는 의미를 엄밀하게 정의하는 데 강하다.
- LPG는 실제 서비스나 분석 시스템에 유연하게 적용하기 좋다.
- 어떤 방식을 선택할지는 표준화 필요성과 실무 활용 목적에 따라 달라진다.

> 한 줄 요약: 온톨로지는 의미를 정의하고, 그래프는 그 의미를 연결 구조로 표현한다.
