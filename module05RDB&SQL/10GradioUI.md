## Gradio UI

### Source

- [AI 기반 SQL 분석 에이전트 구축 - 12. Gradio UI](https://siapapa.github.io/day2/12-gradio-ui/)

### 1. 왜 Gradio인가? -- 프레임워크 비교

강의에서 비교한 핵심 포인트는 다음과 같다.

| 프레임워크 | 코드량 | Colab 지원 | 공유 URL | 학습 곡선 |
| --- | --- | --- | --- | --- |
| **Gradio** | 5줄 | O | O (자동) | 매우 쉬움 |
| Streamlit | 20줄 | X (터널 필요) | X | 보통 |
| Flask/FastAPI | 100줄+ | X | X | 어려움 |
| React | 500줄+ | X | X | 매우 어려움 |

왜 Gradio가 좋은가:

- 웹 개발 지식 없이도 채팅 UI를 빠르게 만들 수 있다
- Colab에서 바로 실행할 수 있다
- `share=True` 한 줄로 공개 URL이 자동 생성된다

> 한 줄 정리: Gradio는 "AI 데모를 가장 적은 코드로 가장 빨리 보여주기 좋은 도구"다.

### 2. Gradio 앱을 Google Drive에 저장하는 방법

강의의 핵심 포인트는 **Colab 노트북 자체가 Gradio 앱 소스코드**라는 점이다.

기본 흐름:

1. Google Drive 마운트
   - `drive.mount('/content/drive')`

2. 노트북을 Drive에 저장
   - `File > Save a copy in Drive`

3. 나중에 다시 실행
   - Drive에서 `.ipynb` 파일 열기
   - `"Open in Colab"` 클릭
   - `Runtime > Run all`

추가 팁:

- 같은 Google 계정이면 Colab Secrets에 저장한 API 키를 다시 불러오기 쉽다.

### 3. 영구 배포가 필요하면 Hugging Face Spaces를 사용하세요

Colab + Gradio 조합은 학습과 데모에는 매우 좋지만, 한계가 있다.

- Gradio 공개 URL은 보통 **72시간 후 만료**
- Colab 런타임이 종료되면 URL도 함께 종료

그래서:

- **실습/프로토타입**: Colab + Gradio
- **영구 공개 배포**: Hugging Face Spaces

로 이해하면 된다.

> 한 줄 정리: Colab의 Gradio URL은 임시 발표용, Hugging Face Spaces는 장기 공개용이다.
