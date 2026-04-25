## Validation, Outliers, And Regression

### Time-Series Cross Validation

- 시계열에서는 일반적인 `k`-fold cross validation처럼 데이터를 무작위로 섞으면 안 된다.
- 시간 순서를 깨뜨리면 데이터 누수(data leakage)가 발생하기 쉽다.

### Common Validation Schemes

- **Rolling 방식**: 학습 구간을 점진적으로 늘리며 다음 구간을 검증한다.
- **Walk-Forward 방식**: 시간 순서를 유지한 채 앞으로 이동하면서 검증한다.

### Sliding Size Choice

- 슬라이딩 크기에는 정답이 없다.
- 데이터 주기성, 예측 길이, 실험 목적, 계산 비용에 맞게 조정해야 한다.
- 실무에서는 `slide=1`을 자주 쓰지만, overlap 문제를 함께 인지해야 한다.

### Outlier Detection

- **Z-score 방식**: 보통 `Z > 3`이면 이상치로 간주한다.
- **STL 분해 기반 방식**: 추세와 계절성을 제거한 뒤 residual을 보고 이상치를 판단한다.

### Regression-Based Time Series Analysis

- 회귀모델을 사용할 때는 설명변수들 사이의 관계도 함께 점검해야 한다.
- 특히 대표적인 문제가 **다중공선성(Multicollinearity)** 이다.

### Multicollinearity

- 독립변수 간 상관관계가 너무 강하면 회귀계수 추정이 불안정해진다.
- 예측 성능이 유지되더라도 계수 해석은 어려워질 수 있다.
- 예를 들어 `Y = β0 + β1X1 + β2X2 + ϵ` 에서 `X1`, `X2`가 매우 유사하면 다중공선성이 발생한다.

> 한 줄 요약: 시계열 실험은 모델 선택만큼이나 검증 방식과 데이터 이상치 처리 설계가 중요하다.
