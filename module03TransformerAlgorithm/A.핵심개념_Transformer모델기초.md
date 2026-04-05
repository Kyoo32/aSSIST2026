## Transformer Master Note: From Model Types to Chat Format

### **1. Transformer 모델 분류: 어떤 구조로 언어를 이해하고 생성하는가**

Transformer 계열 모델은 입력을 어떻게 읽고, 어떤 방식으로 다음 출력을 만드는지에 따라 크게 세 가지로 나눌 수 있습니다.

| 분류 | 핵심 구조 | 대표 목적 |
| --- | --- | --- |
| **Encoder Only** | 입력을 양방향으로 이해 | 이해, 분류, 마스킹 복원 |
| **Decoder Only** | 이전 토큰만 보고 다음 토큰 생성 | 생성, 대화, 자동완성 |
| **Encoder-Decoder** | 입력을 인코딩하고 출력을 디코딩 | 번역, 요약, 질의응답 |

* **Encoder Only LLM:** 대표적으로 **Masked Language Model** 방식입니다. 문장 일부를 가리고, 가려진 토큰을 맞히도록 학습합니다.
* **Decoder Only LLM:** 대표적으로 **Causal Language Model** 방식입니다. 앞에서 나온 토큰만 보고 다음 토큰을 예측합니다.
* **Encoder-Decoder LLM:** 대표적으로 **Seq-to-Seq Language Model** 방식입니다. 입력 시퀀스를 읽고, 다른 형태의 출력 시퀀스를 생성합니다.

> **직관:** Encoder Only는 "문장을 이해하는 두뇌", Decoder Only는 "문장을 이어 쓰는 두뇌", Encoder-Decoder는 "읽고 다시 말해주는 두뇌"에 가깝습니다.

---

### **2. 기본 개념: BF16과 Synthetic Data**

#### **2-1. BF16**

* **BF16 (bfloat16)** 는 16비트 부동소수점 형식 중 하나입니다.
* 실무에서는 메모리 사용량을 줄이고 학습 및 추론 효율을 높이기 위해 자주 사용됩니다.
* 전통적으로 훈련은 `FP32`를 기준으로 생각하는 경우가 많지만, 최근 대형 모델에서는 BF16도 매우 흔하게 사용됩니다.

핵심은 **정밀도와 효율 사이의 균형**입니다.  
모든 계산을 무조건 32비트로 하는 대신, 충분한 성능을 유지하면서 더 빠르고 가볍게 돌리는 방향으로 가는 것입니다.

#### **2-2. Synthetic Unanswerable Math**

* 사람이 직접 모든 데이터를 만들기 어려울 때, 합성 데이터(Synthetic Data)를 활용해 학습 데이터를 구성할 수 있습니다.
* **Synthetic Unanswerable Math**는 모델이 단순 암기만 하지 않고, 문제를 보고 답할 수 있는지 혹은 답할 수 없는 상황을 구분할 수 있는지를 훈련시키는 맥락에서 이해할 수 있습니다.

즉, 모델에게 공식 자체를 노출하지 않아도 **패턴 추론과 응답 태도**를 함께 학습시키려는 접근으로 볼 수 있습니다.

---

### **3. 모델 사용 구조: `pipeline = processor + model`**

Hugging Face 스타일의 사용 흐름에서는 보통 다음 구조를 자주 보게 됩니다.

* **`model`**: 특정 태스크를 수행하도록 학습된 실제 신경망
* **`tokenizer` 또는 `processor`**: 입력을 모델이 이해할 수 있는 형식으로 바꾸는 모듈
* **`pipeline`**: 전처리와 모델 추론을 한 번에 묶어 쓰기 쉽게 만든 인터페이스

즉,

`pipeline = processor + model`

처럼 이해할 수 있습니다.

텍스트만 다룰 때는 tokenizer가 중심이지만, 이미지나 오디오까지 다루는 멀티모달 환경에서는 processor가 더 넓은 개념으로 쓰입니다.

---

### **4. Transformer 내부 구성요소: 임베딩과 드롭아웃**

강의 메모에 나온 축약어들은 보통 다음처럼 이해하면 됩니다.

* **`wte` (word/text embedding):** 텍스트 토큰을 벡터로 바꾸는 임베딩
* **`wpe` (position embedding):** 토큰의 순서 정보를 반영하는 위치 임베딩
* **`drop` (dropout):** 학습 중 일부 연결을 무작위로 비활성화해 과적합을 줄이는 기법

Transformer는 단어의 의미만 보는 것이 아니라, **어떤 순서에 놓였는지**도 같이 알아야 하므로 `wte`와 `wpe`가 함께 중요합니다.

> **직관:** `wte`가 "이 단어가 무엇인가"를 알려준다면, `wpe`는 "이 단어가 문장 안에서 몇 번째인가"를 알려줍니다.

---

### **5. Multi-turn / Multi-modal Chat 만들기**

대화형 모델을 사용할 때는 입력을 단순 문자열 하나로 넣는 대신, **역할(role)** 과 **대화 순서**를 갖춘 메시지 구조로 만드는 경우가 많습니다.

기본 role은 다음과 같습니다.

* **system:** 모델의 전체 행동 규칙이나 지침
* **user:** 사용자의 질문이나 요청
* **assistant:** 모델의 응답

멀티턴 채팅에서는 이 메시지들이 순서대로 누적되며, 모델은 이전 대화 맥락을 참고해 다음 응답을 생성합니다.

멀티모달 채팅에서는 여기에 텍스트뿐 아니라 이미지, 오디오 등 다른 입력 형식도 함께 들어갈 수 있습니다.  
이때 processor는 여러 modality를 공통된 모델 입력 형식으로 변환하는 역할을 합니다.

예를 들면 다음과 같이 이해할 수 있습니다.

```python
messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "이 이미지를 설명해줘."},
    {"role": "assistant", "content": "이미지에는 ..."}
]
```

이 구조는 단순해 보이지만, 실제로는 **맥락 유지**, **지침 반영**, **멀티턴 일관성**을 만드는 핵심 포맷입니다.

---

### **6. 한 번에 정리하는 흐름**

1. Transformer 모델은 Encoder Only, Decoder Only, Encoder-Decoder로 나뉜다.
2. Encoder Only는 이해 중심, Decoder Only는 생성 중심, Encoder-Decoder는 변환 중심이다.
3. 모델 사용 시에는 `processor/tokenizer`가 입력을 바꾸고, `model`이 실제 추론을 수행한다.
4. `wte`, `wpe`, `dropout`은 Transformer 내부 이해의 기본 구성요소다.
5. 멀티턴 채팅은 `system`, `user`, `assistant` role 구조로 관리된다.
6. 멀티모달 채팅은 processor가 여러 입력 형식을 함께 다룰 수 있게 해준다.

Transformer를 이해하는 핵심은 결국, **입력을 어떻게 표현하고, 어떤 방향으로 다음 출력을 만들도록 학습시키는가**를 보는 것입니다.
