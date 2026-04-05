<transformer 모델 분류>
* Encoder Only LLM: Mask Language Model
* Decoder Only LLM: Causal Language Model
* Encoder-Decoder LLM: Seq-to-Seq Language Model

<개념>
* BF16: brain floating 16. 보통 훈련은 32bit. 파라미터에 곱해야함
* Synthetic Unanswerable Math: 공식을 알려주지 않아도 대답하는 훈련

<모델 사용>
* pipeline = processor + model
* model = task 수행 훈련된 모델
* tokenizer(processor) = 토큰화 모듈

wte: text embedding
wpe: position embedding
drop: Dropout

### How to make Multi-turn/Multi-modal Chat
* role: system / user / assistant
