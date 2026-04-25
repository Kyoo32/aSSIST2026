## Transformer Algorithm

### Topic Map

- `01TransformerBaseAndFamilies.md`: Transformer 기반 모델의 분류와 전체 관점
- `02TokenizerEmbeddingAndAttention.md`: 토크나이저, 임베딩, self-attention 핵심
- `03TrainingPostTrainingAndReasoning.md`: 학습, post-training, reasoning, 모델 사용 구조
- `04ScalingNormalizationAndResidual.md`: scaling, normalization, residual, FFN, LM head
- `05PositionalEncodingChatAndApplications.md`: positional encoding, 멀티턴 채팅, 대표 응용

### Quick Summary

1. Transformer의 공통 핵심은 self-attention이다.
2. 모델 구조는 encoder-only, decoder-only, encoder-decoder로 나뉜다.
3. 입력 표현은 tokenizer, embedding, positional encoding이 담당한다.
4. 학습 안정성은 normalization, residual connection, scaling이 좌우한다.
5. 실제 활용은 chat format, multimodal processor, application model까지 확장된다.
