# 7강

# 목차


## Fancier optimization

### Problems with SGD
- 가중치 변수가 2개 있을때 loss가 특정 가중치에는 민감하게 반응하고 다른 가중치에는 약하게 반응할때 로스함수 그래프는 지그재그 형태를 보임.
- 고차원 공간일수록 위와 같은 문제가 더 자주 일어남.
- local minima 와 saddle point 에서 gradient 가 0 이 되어버리는 문제가 발생함
- 고차원공간일수록 saddle point 에 더 취약함
- 가중치의 위치가 saddle point 근처면 업데이트가 굉장히 느리게 진행됨(gradient가 작아서)

### SGD + Momentum
SGD에서 보이는 문제점을 해결하려고 나온 개념
- velocity 값을 사용해 gradient 가 0이어도 학습이 진행 될 수 있게함
- high condition number prob lem을 해결함.

## Regularization

## Transfer Learning