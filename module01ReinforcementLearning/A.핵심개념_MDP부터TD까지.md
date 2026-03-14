## Reinforcement Learning Master Note: From MDP to TD

<img width="3664" height="1120" alt="Gemini_Generated_Image_5aso2p5aso2p5aso" src="https://github.com/user-attachments/assets/decb229f-bb08-46cf-a8b4-76141c53df8b" />


### **1. MDP (Markov Decision Process): 세계관의 정의**

MDP는 의사결정 문제를 수학적으로 정의한 **프레임워크**입니다.

* **구성 요소 ($S, A, P, R, \gamma$):**
* **State ($S$):** 에이전트가 관찰하는 현재 상황.
* **Action ($A$):** 에이전트가 취할 수 있는 선택지.
* **Transition Probability ($P$):** 상태 $s$에서 행동 $a$를 했을 때 다음 상태 $s'$로 갈 확률 $P(s'|s, a)$.
* **Reward ($R$):** 행동의 결과로 받는 즉각적인 피드백.
* **Discount Factor ($\gamma$):** 미래 보상의 현재 가치를 결정하는 비율 ($0 \le \gamma \le 1$).


* **Stochastic Task:** 현실은 결정론적이지 않으며, 같은 행동도 확률적 전이에 의해 결과가 달라집니다.

> **📸 한 줄 비유:** MDP는 게임의 **'룰북'**입니다. 어떤 규칙으로 세상이 돌아가는지 정의합니다.

---

### **2. Bellman Equation: 가치 계산의 도구**

벨만 방정식은 현재 상태와 다음 상태 가치 사이의 **재귀적 관계**를 나타내는 수식입니다.

* **Bellman Expectation Equation (평가):** 현재 정책 $\pi$를 따랐을 때의 기대 가치입니다.

$$V_\pi(s) = \sum_{a \in A} \pi(a|s) \sum_{s' \in S, r \in R} p(s', r|s, a) [r + \gamma V_\pi(s')]$$


* **Bellman Optimality Equation (제어):** 가장 똑똑하게 행동했을 때 얻을 수 있는 최대 가치입니다.

$$V^{opt}(s) = \max_{a \in A} \sum_{s', r} p(s', r | s, a) [r + \gamma V^{opt}(s')]$$


> **📸 한 줄 비유:** 벨만 방정식은 게임의 '점수 계산기'입니다. 지금 내 위치가 수학적으로 얼마나 유리한지 알려줍니다.

---

### **3. MC vs TD: 경험을 통한 학습 알고리즘**

모델($P, R$)을 모를 때, 실제 경험을 통해 벨만 방정식을 풀어가는 방식입니다.

| 구분 | **MC (Monte Carlo)** | **TD (Temporal Difference)** |
| --- | --- | --- |
| **핵심 개념** | 에피소드가 **끝나야** 업데이트 | 한 스텝마다 **즉시** 업데이트 (Bootstrapping) |
| **수식** | $V(s) \leftarrow V(s) + \alpha [G_t - V(s)]$ | $V(s) \leftarrow V(s) + \alpha [r + \gamma V(s') - V(s)]$ |
| **장단점** | 편향(Bias)이 없으나 분산(Var)이 높음 | 분산이 낮으나 초기 편향이 존재할 수 있음 |
| **비유** | **'인생 복기'**: 죽기 직전에 삶을 돌아봄 | **'오답 노트'**: 매일 한 문제 풀고 바로 채점함 |

---

### **4. 핵심 키워드 및 알고리즘**

* **Argmax ($\arg\max$):** 최댓값을 만드는 **'인자(행동)'** 를 찾는 연산입니다. 정책 최적화의 핵심입니다.
* **Exploration vs Exploitation:**
    * **Exploration (탐험):** 더 큰 보상을 위해 새로운 길을 시도하는 것 (초기 전략).
    * **Exploitation (활용):** 아는 정보 중 최선의 행동을 반복하는 것 (중기 전략).


* **TD-gammon:** 인공신경망과 TD 학습을 결합하여 백개먼을 정복한 현대 Deep RL의 조상 격 모델입니다.

---

### **5. 인생을 위한 RL의 통찰 (Philosophy)**

수학적 모델은 단순한 코드를 넘어 우리 삶에 중요한 전략을 제시합니다.

1. **결과가 아닌 정책 최적화:** 결과는 확률적(Stochastic)이지만, 행동 지침(Policy)은 우리가 통제할 수 있습니다.
2. **보상 함수(Reward Function) 설계:** 내가 무엇에 가치를 두느냐에 따라 뇌의 모든 선택 알고리즘이 바뀝니다.
3. **지속적 업데이트:** 우리는 끊임없이 경험하고 정책을 업데이트하는 **Lifelong Learner**입니다.

---






