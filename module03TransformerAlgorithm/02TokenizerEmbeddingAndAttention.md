## Tokenizer, Embedding, And Attention

### Tokenizer

- 토크나이저는 텍스트를 모델이 처리할 수 있는 토큰 단위로 나눈다.
- 실무적으로는 **subword** 방식이 가장 널리 쓰인다.
- 자주 나오는 표현은 의미 단위로, 나머지는 더 작은 단위로 쪼개 신조어에도 대응할 수 있다.
- 대표적인 사전 구축 방식은 **BPE (Byte Pair Encoding)** 이다.

### Embedding And Representation

- 임베딩은 토큰을 벡터 공간으로 옮기는 과정이다.
- 딥러닝은 사람이 직접 feature를 정하기보다, 학습을 통해 표현(representation)을 찾는다.
- 잠재공간(latent space)은 텍스트, 이미지, 소리 같은 정보를 수치화한 공간이다.
- 좋은 표현 공간이 만들어지면 분류, 회귀, 생성이 쉬워진다.

### Useful Terms

- `wte`: text embedding
- `wpe`: position embedding
- `drop`: dropout

### AutoEncoder Family

- **AutoEncoder**: 입력을 압축했다가 복원하며 표현을 학습한다.
- **VAE**: 확률적 잠재공간을 사용해 더 부드럽고 안정적인 생성에 유리하다.

### Attention

- Attention은 문맥 속에서 어떤 토큰이 중요한지 가중치를 두는 메커니즘이다.
- Self-attention은 입력 내부의 토큰들끼리 서로 참고하도록 만든다.
- 결과적으로 토큰은 **context-aware vector**가 된다.
- 의미가 비슷한 토큰은 attention을 통해 더 비슷한 표현으로 정렬될 수 있다.

### Historical Flow

- Word2Vec 이후 표현 학습이 발전했다.
- Attention 아이디어가 등장했고,
- 2017년 Transformer가 이를 핵심 구조로 정착시켰다.

> 핵심 직관: Transformer는 단어를 혼자 보지 않고, 다른 단어들과의 관계 속에서 다시 표현한다.
