# HGF (Hierarchical Gaussian Filter)
# 2. HGF 모델 설명

[[그림]] </bar>

한 agent가 그림과 같이 불빛의 상태를 관찰한다고 가정하자. 불빛은 1초마다 한 번씩 나타나거나/나타나지 않는다.(x1)  </br></br>
이 때, agent는 불빛이 나타나면 불빛이 보인다고 지각하고, 불빛이 나타나지 않으면 불빛이 보이지 않는다고 지각한다. (input u = x1) </br>*(이렇게 perceptual uncertainty가 없는 상태를 deterministic하다고 한다; 나중에 perceptual uncertainty가 있는 상황을 살펴볼 것이다)* </br></br>
agent는 이 불빛이 반짝이는 상태를 보고 불빛의 경향성이 어떻게 되는지를 알고 싶어한다. 이 불빛의 경향성을 x2라고 하면 x2는 x1=1일 확률(불빛이 나타날 확률)로 볼 수 있다. </br>즉, P(x_1=1) = s(x_2) (s = sigmoid(softmax)) 
</br></br>
이때, x2는 Gaussian random walk로 시간에 따라 변화한다고 가정한다. 즉, 시간 k에서 x2의 확률은 시간 k-1에서의 x2를 평균으로 하는 정규분포를 그린다고 본다. 이를 수식으로 나타내면 다음과 같다.
</br>
[[수식]]
</br>


