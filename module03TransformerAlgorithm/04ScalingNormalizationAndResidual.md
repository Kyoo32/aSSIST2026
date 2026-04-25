## Scaling, Normalization, And Residual

### Scaling

- 값의 스케일 차이가 크면 작은 패턴이 묻힐 수 있다.
- 따라서 attention과 깊은 네트워크에서는 적절한 scaling이 중요하다.

### Normalization

- normalization은 값이 폭주하는 현상을 줄이고 학습을 안정화한다.
- 깊은 레이어를 쌓을수록 gradient 전달이 약해질 수 있다.
- 이런 문제는 vanishing gradient와 연결된다.
- 최근에는 **RMSNorm** 계열도 자주 사용된다.

### Residual Connection

- residual connection은 skip connection이라고도 부른다.
- 레이어를 건너뛰는 경로를 추가해 정보와 gradient 흐름을 더 잘 유지한다.
- 매우 깊은 모델에서 필수적인 안정화 장치다.
- 최근에는 deep hyper connection 같은 확장 개념도 등장한다.

### Feed Forward Network

- Transformer block의 FFN은 attention 뒤에서 표현을 다시 가공한다.
- 이 레이어는 파라미터 비중이 커서 효율화 대상이 되기 쉽다.
- 대표적인 효율화 방향이 **MoE (Mixture of Experts)** 이다.

### LM Head

- LM Head는 다음 토큰의 확률을 예측하는 출력부다.
- 일반적으로 `Linear + Softmax` 구조로 이해할 수 있다.
- 구조화된 출력이 필요할 때는 Pydantic 같은 포맷 제약과 함께 활용되기도 한다.

> 한 줄 요약: 깊고 큰 Transformer를 안정적으로 학습시키는 핵심은 normalization, residual, 그리고 효율적인 FFN 설계다.
