# 7강

# 목차

1. [Fancier optimization](#fancier-optimization)

2. [Model Ensembles](#model-ensembles)

3. [Regularization](#regularization)

4. [Transfer Learning](#transfer-learning)
5. 
## Fancier optimization
First Order (1차 미분)
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

### Nesterov Momentum
SGD + Momentum 에서 발생하는 문제점을 해결하기 위한 모멘텀
- velocity 를 구하는 공식에 러닝레이트를 추가시킴
- 일반 momentum에 비해 overshooting이 덜 함.
- u*vt 만큼이동한 지점의 gradient를 구함.

### AdaGrad
훈련도중 계산되는 gradients를 활용하는 방법
- small dimension에서는 gradient의 제곱 값 합이 작음 (가속도가 붙음)
- large dimension에서는 gradient의 제곱 값 합이 큼 (속도가 점점 줄어들음)
- 일반적으로 Neural Network를 학습시킬 때 AdaGrad를 잘 사용하지 않음.

### Problem of AdaGrad
-  학습이 진행 될 수록 나아가는 값이 점점 작아짐
-  convex case 에서는 좋은 특징
-  non-convex case는 나쁜 특징 (saddle point 에 걸려버릴 수 있음)

### RMSProp
AdaGrad의 변형버전
- AdaGrad의 gradient 제곱 항을 그대로 사용
- 값들을 그저 누적시키기 보단 기존의 누적값에 decay_rate를 곱해줌
- decay rate의 값은 보통 0.9 혹은 0.99를 사용함
- gradient 제곱을 계속 나눠준다는 점에서 AdaGrad와 유사함


### Adam 
- 두 종류의 모멘텀을 사용함
- RMSProp + momentum 의 개념
- first moment 와 second moment의 초기값은 0
- 첫번째 step 에서 second moment의 값은 여전히 0 에 가까움
- 첫번째 step size 의 크기가 커지는 걸 방지하기 위해서 bias 값을 추가함
- 일반적으로 Adam 으로 학습을 시작하는것이 좋음

### Learning rate decay
- Adam 보다는 SGD Momentum을 사용할 때 자주 씀.
- second-order(부차적인) parameter임. 학습 초기부터 고려하지 않음.


### Etc
- full batch update가 가능하고 stochasticity가 적은 경우라면 L-BFGS가 좋은 선택이 될 수 있음.
- style transfer 와 같은 알고리즘에서 L-BFGS를 종종 사용할 수 있음

## Model Ensembles
모델을 하나만 학습시키지 않고 10개의 모델을 독립적으로 학습시킴 (train 과 test 셋에서의 정확도를 일치시키기 위한 방법중 하나)
- 모델의 수가 늘어날수록 overfitting 이 줄어들고 성능이 조금씩 향상됨.
## Regularization
단일 모델의 성능을 올려주는 방법론중 하나
- 모델이 training data에 fit 하는 것을 막아줌


### Dropout
forward pass 과정에서 임의로 일부 뉴런의 activation값을 0으로 만들어줌.
- 일반적으로 fc-layer에서 사용되지만 conv net 에서도 가끔 사용됨.
- conv layer의 경우 여러 channel 이 있기 때문에 일부 channel 자체를 dropout 시킬 수도 있음.
- 특징들간의 상호작용을 방지함.
- 네트워크가 일부 feature에만 의존하지 못하게 함.
- backpropagation 과정에서 Dropout이 0으로 만들지 않은 노드에서만 연산이 이뤄짐.
- 각 스텝마다 업데이트되는 파라미터 수가 줄어들기 대문에 학습시간이 늘어남.
- 전체 학습시간은 늘어나지만 모델이 수렴한 이후에는 더 좋은 일반화 능력을 얻을 수 있음.
- 보통 BN(Batch-Normalization) 을 사용할때 Dropout을 사용하지 않음

### Test time 에서의 dropout
- test time 에 임의의 값을 부여하는 것은 좋지 않음.
- 랜덤한 정도를 average out 시킬때 적분을 사용하지만 쉽지않음
- 적분식을 사용하는 대신 dropout 확률값을 곱해줘서 local approximation 시키는 방법이 있음.

### Data augmentation
원본 이미지의 방향 스케일 등을 바꿔서 일반화 시키는 방법
- scaling
- color jiltering
- rotation
- cropping
- translation
- shearing
- lens distortions

## Transfer Learning
충분한 데이터가 없을 때 아주 작은 데이터셋에 대해 지나치게 overfit할때 쓰는 방법

||very similar dataset|very different dataset|
|------|---|---|
|very little data|Use Linear Classifier on top layer|Try linear classifier from different stages|
|quite a lot of data|Finetune a few layers|Finetune a larger number of layers|