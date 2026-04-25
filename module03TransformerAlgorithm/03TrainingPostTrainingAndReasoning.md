## Training, Post-Training, And Reasoning

### Transformer Training Flow

- 기본 구성은 다음 흐름으로 볼 수 있다.

1. Tokenizing
2. Input Embedding
3. Positional Embedding
4. Self Attention
5. Multi-Head Attention
6. Add & Normalize
7. Feed Forward
8. Linear & Softmax

### Teacher Forcing

- Teacher forcing은 학습 시 이전 단계의 예측값 대신 정답 토큰을 넣는 방식이다.
- 학습을 안정화하고 병렬 학습에 유리하다.

### GPT Lineage

- GPT 계열은 self-supervised learning 기반이다.
- InstructGPT는 RLHF를 통해 human feedback을 보상 모델에 반영했다.
- ChatGPT는 instruction following과 moderation 레이어를 포함한 대화형 사용에 최적화된 형태로 볼 수 있다.

### Post-Training

- Post-training에서는 데이터 품질이 특히 중요하다.
- 사전학습만으로는 충분하지 않고, 정렬(alignment)과 사용성 개선 단계가 필요하다.

### Reasoning

- 최근 Transformer 연구는 단순 생성에서 reasoning 능력 강화로 이동하고 있다.
- 답만 맞히는 것이 아니라, 맥락을 유지하고 적절한 추론 경로를 따르는지가 중요해졌다.

### Model Usage

- `pipeline = processor + model`
- `model`: 특정 task를 수행하도록 훈련된 모델
- `tokenizer` 또는 `processor`: 입력을 모델 형식으로 바꾸는 모듈

### Extra Concepts

- **BF16 (bfloat16)**: 메모리 사용량과 연산 효율을 개선하기 위해 널리 쓰이는 숫자 표현 형식
- **Synthetic Unanswerable Math**: 공식 암기보다 응답 가능성과 추론 태도를 함께 학습시키려는 데이터 설계로 이해할 수 있다

> 핵심 포인트: 사전학습은 지식을 넓히고, post-training은 그 지식을 더 잘 쓰게 만든다.
