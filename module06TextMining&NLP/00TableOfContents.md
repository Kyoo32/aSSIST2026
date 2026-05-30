## Text Mining And NLP

### Topic Map

- [01LanguageModelsAndTransformerBasics.md](01LanguageModelsAndTransformerBasics.md): 언어모델 정의, Transformer 구조, GPT와 pretraining 기초
- [02ModelUsageRetrievalAndReranking.md](02ModelUsageRetrievalAndReranking.md): 모델 설정 읽기, tokenizer/chat template, 검색기와 리랭킹
- [03EmbeddingTrainingAndRetrievalEvaluation.md](03EmbeddingTrainingAndRetrievalEvaluation.md): 포지티브·네거티브 샘플, 대조학습, 검색 평가 지표
- [04DataPreparationFineTuningAndAgents.md](04DataPreparationFineTuningAndAgents.md): 데이터 정제, LoRA 중심 파인튜닝, 에이전트 관점

### Quick Summary

1. 언어모델은 가장 자연스러운 다음 단어를 예측하는 구조에서 출발한다.
2. Transformer는 encoder, decoder, encoder-decoder 관점으로 나눠 이해할 수 있다.
3. RAG와 검색 품질은 임베딩, BM25, 하이브리드, 리랭킹 조합에 크게 좌우된다.
4. 임베딩 학습은 포지티브와 네거티브 샘플을 이용한 대조학습으로 설명할 수 있다.
5. 검색 평가는 정답 포함 여부, 정밀도, 순위 품질을 함께 봐야 한다.
6. 실무에서는 데이터 정제와 LoRA 같은 자원 효율 파인튜닝이 중요하다.
7. 에이전트는 LLM에 도구 사용과 실행 흐름을 붙인 확장 구조로 볼 수 있다.
