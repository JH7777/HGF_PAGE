# HGF (Hierarchical Gaussian Filter)
## 1. 왜 HGF를 사용하는가
학습은 주변 환경에 대한 agent의 믿음이 이미 알고 있던 정보와 새로운 정보를 통합함으로써 향상되는 과정으로 이해할 수 있다. 


이러한 학습을 이해하는데 현재 크게 두가지의 메커니즘(Reinforcement Learning, Bayesian Learning)이 사용된다. 그러나 이 두 메커니즘은 각각 여러가지 단점을 가진다. 여기서 설명할 HGF는 그러한 단점을 보완하기 위하여 설계되었다. 먼저 각각의 알고리즘이 무엇인지, 그리고 단점은 어떤 것이 있는지 살펴보자.

### Bayesian Learning


P(A|B)=\frac { P(B|A)P(A) }{ P(B) } 


이 식은 베이즈 정리식이다. 이 식에서 B는 관측된 data, A는 불확실성을 계산하고자 하는 대상으로 볼 수 있다. 따라서 

  `* P(A)`는 불확실성을 계산하고자 하는 대상의 **사전 확률** (과거의 경험으로 알 수 있다)</br>
  `* P(B)`는 data의 사전확률 (정규화 상수 역할을 한다; 현재의 증거라는 의미에서 **evidence**라고도 한다)</br>
  `* P(B|A)`는 A에 따라 data가 관측될 조건부 확률 (A에 대한 과거의 경험에 기초한 data가 관측될 확률; **likelihood**라고도 한다.)</br>
  `* P(A|B)`는 이러한 data(B)가 관측되었을 때 A의 확률 (구하고자 하는 **사후확률**)</br>


따라서 Bayesian learner은 A의 사전확률 P(A)를 알고 있을 때 data(B)를 관측함으로써 A의 확률(P(A|B))을 업데이트 시켜나간다. 
즉, **A의 사후확률**을 구한다.


그러나 이 이론은 몇가지 단점을 가지고 있다.

1. P(A|B)를 계산하기 위해서는 위의 수식에서 P(B)를 계산해야 한다. 이 값은 P(B)=\int_{A} {P(B|A)}를 계산함으로써 얻을 수 있다. 그러나 매우 간단한 경우를 제외하고는 이 적분을 계산하기는 매우 복잡하다. 따라서 이 적분은 실제로 agent가 정보 하나가 들어올 때 마다 수행한다고 보기 어렵다.
2. Bayesian leaning은 정보가 어떻게 다루어져야 하는지를 규정하는 normative framework를 구성한다. 그러나 실제 상황에서는 만약 모든 agent가 같은 prior knowledge를 가지고 있더라도 새로운 정보를 똑같이 받아들이지 않는다. 즉, Bayesian Learning은 inter-individual variability를 무시한다.


### Reinforcement Learning (RL)
* Bayesian learning이 normative framework를 가지고 있는 반면, Reinforcement Learning은 descriptive 접근법을 사용한다. 즉, 어떠한 확률 이론을 가정하지 않고 그저 agent가 다른 자극과 행동으로부터 "value"를 학습하는 과정을 기술한다.

