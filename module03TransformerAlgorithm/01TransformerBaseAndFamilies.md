## Transformer Base And Families

### Transformer Base

- Transformer 기반 모델은 대부분 자기지도학습(self-supervised learning)을 수행한다.
- 대표 예시는 ChatGPT, LLaMA, BERT 계열이며, LLM과 FM의 다수가 Transformer 기반이다.
- NLP뿐 아니라 ViT, SAM처럼 비전 영역에도 널리 확장되었다.
- 핵심 메커니즘은 **self-attention**이다.

### Model Families

| 계열 | 학습 방식 | 주 용도 |
| --- | --- | --- |
| **Encoder Only** | Masked Language Modeling | 이해, 분류, 표현 학습 |
| **Decoder Only** | Causal Language Modeling | 생성, 대화, 자동완성 |
| **Encoder-Decoder** | Seq-to-Seq | 번역, 요약, 변환 |

- **Encoder Only LLM**: 문장 일부를 가리고 복원하는 방식에 강하다.
- **Decoder Only LLM**: 앞의 토큰만 보고 다음 토큰을 예측한다.
- **Encoder-Decoder LLM**: 입력을 읽고 다른 형태의 시퀀스로 바꾸는 데 적합하다.

### Why Transformer Matters

- 일반화 성능이 뛰어나고 fine-tuning에도 유리하다.
- 같은 기본 구조를 다양한 데이터 형태에 재사용할 수 있다.
- Attention 기반이므로 긴 문맥 관계를 더 직접적으로 다룰 수 있다.

> 한 줄 요약: Transformer는 "어떤 요소가 지금 중요한가"를 동적으로 고르는 범용 표현 학습기다.
