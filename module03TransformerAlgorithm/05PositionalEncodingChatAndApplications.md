## Positional Encoding, Chat Format, And Applications

### Positional Information

- Transformer는 순서를 자동으로 알지 못하므로 위치 정보가 필요하다.
- 위치 임베딩은 각 토큰이 문장 안에서 어디 있는지 알려준다.

### RoPE

- **RoPE (Rotary Positional Embedding)** 는 회전 행렬을 이용해 상대적 위치 정보를 반영한다.
- 긴 문맥에서 위치 관계를 더 자연스럽게 다루는 데 유리하다.
- 패딩으로 인한 비효율을 줄이는 방향과도 잘 맞는다.

### Multi-turn / Multi-modal Chat

- 멀티턴 채팅은 메시지를 역할(role) 단위로 누적해 구성한다.
- 기본 role은 다음과 같다.
  - system
  - user
  - assistant
- 멀티모달 환경에서는 processor가 텍스트, 이미지, 오디오 입력을 함께 다룬다.

### Memory Perspective

- 최근에는 memory를 context로 다루는 방향도 강화되고 있다.
- Titans 같은 아이디어는 새로운 정보 업데이트와 장기 기억을 분리해 보려는 시도로 이해할 수 있다.
- 비유적으로는 해마가 contextual memory, 대뇌피질이 persistent memory 역할을 담당하는 구조와 닮아 있다.

### Applications

- **SAM (Segment Anything Model)**: Transformer 계열이 비전에서 어떻게 확장되는지 보여주는 대표 사례
- **ViT**: Transformer를 이미지 처리에 적용한 기본 사례
- LLM, VLM, FM 모두 Transformer 기반 확장의 연장선에 있다

> 핵심 메시지: Transformer는 텍스트 모델을 넘어, 메모리와 멀티모달 상호작용까지 포괄하는 공통 인터페이스로 진화하고 있다.
