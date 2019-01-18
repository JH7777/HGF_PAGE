# HGF (Hierarchical Gaussian Filter)
# 1. 왜 HGF를 사용하는가
학습은 주변 환경에 대한 agent의 믿음이 이미 알고 있던 정보와 새로운 정보를 통합함으로써 향상되는 과정으로 이해할 수 있다. 


이러한 학습을 이해하는데 현재 크게 두가지의 메커니즘(***Reinforcement Learning, Bayesian Learning***)이 사용된다. 그러나 이 두 메커니즘은 각각 여러가지 단점을 가진다. 여기서 설명할 HGF는 그러한 단점을 보완하기 위하여 설계되었다. 먼저 각각의 알고리즘이 무엇인지, 그리고 단점은 어떤 것이 있는지 살펴보자.

## Bayesian Learning


P(A|B)=\frac { P(B|A)P(A) }{ P(B) } 


이 식은 베이즈 정리식이다. 이 식에서 B는 관측된 data, A는 불확실성을 계산하고자 하는 대상으로 볼 수 있다. 

  `* P(A)`는 불확실성을 계산하고자 하는 대상의 **사전 확률** (과거의 경험으로 알 수 있다)</br>
  `* P(B)`는 data의 사전확률 (정규화 상수 역할을 한다; 현재의 증거라는 의미에서 **evidence**라고도 한다)</br>
  `* P(B|A)`는 A에 따라 data가 관측될 조건부 확률 (A에 대한 과거의 경험에 기초한 data가 관측될 확률; **likelihood**라고도 한다.)</br>
  `* P(A|B)`는 이러한 data(B)가 관측되었을 때 A의 확률 (구하고자 하는 **사후확률**)</br>


따라서 Bayesian learner은 A의 사전확률 P(A)를 알고 있을 때 data(B)를 관측함으로써 A의 확률(P(A|B))을 업데이트 시켜나간다. 
즉, **A의 사후확률**을 구한다. </br></br>


그러나 이 이론은 몇가지 단점을 가지고 있다.

1. P(A|B)를 계산하기 위해서는 위의 수식에서 P(B)를 계산해야 한다. 이 값은 P(B)=\int_{A} {P(B|A)}를 계산함으로써 얻을 수 있다. 그러나 매우 간단한 경우를 제외하고는 이 적분을 계산하기는 매우 복잡하다. 따라서 이 적분을 실제로 agent가 정보 하나가 들어올 때 마다 수행한다고 보기 어렵다.*(현실적이지 않다.)*
2. Bayesian leaning은 정보가 어떻게 다루어져야 하는지를 규정하는 normative framework를 구성한다. 그러나 실제 상황에서는 만약 모든 agent가 같은 prior knowledge를 가지고 있더라도 새로운 정보를 똑같이 받아들이지 않는다. 즉, Bayesian Learning은 inter-individual variability를 무시한다.*(베이즈 정리 식에서 individual 정보를 주는 부분은 없다.)*


## Reinforcement Learning (RL)
[[연합강도 그림]] </br>
고전적 조건형성에서 CS와 UCS의 연합강도를 V라고 둘 수 있다. 이 연합강도 V는 시행이 반복될 수록 강해지지만 무작정 강해지지는 않고 그림에서 볼 수 있듯이 로그 함수꼴로 증가한다. 이 때 시행을 한 번 할 때마다 연합강도의 변화량을 \Delta V라고 하면 \Delta V_n \sim  V_{max}-V_n, 즉 \Delta V는 V_{max}-V_n에 비례한다. </br>
이 식은 최대 연합강도와 현재의 연합강도의 차이가 클 때는 학습이 빨리 일어나지만 현재의 연합강도가 최대 연합강도와 비슷할 때는 학습이 잘 되지 않음을 의미한다. </br>이 때, 상수 C를 포함시키면 이 식은 \Delta V_n=c(V_{max}-V_n)로 나타낼 수 있는데, c는 learning rate *(individual 마다 다른 값을 가진다)* 이다. </br></br>
이 이론은 다음과 같은 특징을 지닌다.
- Bayesian learning이 normative framework를 가지고 있는 반면, Reinforcement Learning은 descriptive 접근법을 사용한다. 즉, 어떠한 확률 이론을 가정하지 않고 그저 agent가 다른 자극과 행동으로부터 "value"를 학습하는 과정을 기술한다. 따라서 조현병과 우을증과 같은 일탈적 학습도 모델링 할 수 있다.
- 개념적으로 간단하고 계산이 간편하다.

</br> 그러나 이 이론에도 중요한 단점이 있다.
- 확률 이론을 따르지 않는 heuristic한 접근법이기 때문에 환경적 상태와 행동의 결과가 agent에게 알려지지 않은 채로 학습해야 하는 실제 상황에 잘 맞지 않는다.

`따라서 업데이트된 Bayesian model(HGF)을 통하여 Bayesian 모델과 RL 모델의 단점을 극복하고자 하였다. 또한 이렇게 업데이트된 Bayesian 식은 RL 모델과 유사한 형태를 띄게 된다.`
