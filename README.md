# HGF (Hierarchical Gaussian Filter)
## 1. 왜 HGF를 사용하는가
#### 학습은 주변 환경에 대한 agent의 믿음이 이미 알고 있던 정보와 새로운 정보를 통합함으로써 향상되는 과정으로 이해할 수 있다. 
#### 이러한 학습을 이해하는데 현재 크게 두가지의 메커니즘(Reinforcement Learning, Bayesian Learning)이 사용된다. 그러나 이 두 메커니즘은 각각 여러가지 단점을 가진다. 여기서 설명할 HGF는 그러한 단점을 보완하기 위하여 설계되었다. 먼저 각각의 알고리즘이 무엇인지, 그리고 단점은 어떤 것이 있는지 살펴보자.

#### 1) Bayesian Learning
##### 간단한 경우를 제외하고는 Bayes's Theorem을 적용하는 것은 복잡한 적분을 요구한다. 이 적분은 실제로 agent가 정보 하나가 들어올 때 마다 수행한다고 하기에는 너무 복잡하다.
##### Bayesian leaning은 정보가 어떻게 다루어져야 하는지를 규정하는 normative framework를 구성한다. 그러나 실제 상황에서는 만약 모든 agent가 같은 prior knowledge를 가지고 있더라도 새로운 정보를 똑같이 받아들이지 않는다. 즉, Bayesian Learning은 inter-individual variability를 무시한다.
#### 2) Reinforcement Learning (RL)
##### Bayesian learning이 normative framework를 가지고 있는 반면, Reinforcement Learning은 descriptive 접근법을 사용한다. 즉, 어떠한 확률 이론을 가정하지 않고 그저 agent가 다른 자극과 행동으로부터 "value"를 학습하는 과정을 기술한다.

