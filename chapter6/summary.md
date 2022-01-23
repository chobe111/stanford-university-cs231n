# 6강

# 목차

1. [Activation Functions](#activation-functions)

2. [Data Preprocessing](#data-preprocessing)

3. [Weight Initialization](#weight-initialization)

4. [Batch Normalization](#batch-normalization)

5. [Babysitting the Learning Process](#babysitting-the-learning-process)

6. [Hyperparameter Optimization](#hyperparameter-optimization)
## Activation Functions

* sigmoid
  - x 가 클수록 y가 1에 근접하고 작아질수록 0에 근접함. [0, -1]
  - 포화상태의 뉴런이 gradient 를 죽임.
  - 그래프의 분포가 zero-centered 가 아님

* neuron 의 값이 항상 음수 / 혹은 양수일 때의 문제점
  - 파라미터를 업데이트 할 때 다 같이 증가/감소함.
  - zero-mean 데이터를 만듦으로써 해당 문제를 해결 할 수 있음.

* tanh(x)
  - x 가 클수록 y 가 1에 근접하고 작아질수록 -1에 근접함. [-1, 1]
  - 그래프의 분포가 zero-centered 임.
  - gradient가 죽는문제가 발생함.

* ReLU (Rectified Linear Unit)
  - 양수에서 포화(saturate)문제가 발생하지 않음.
  - 지수항이 없기 때문에 계산이 매우 빠름.
  - sigmoid,tanh 보다 수렴속도가 훨씬 빠름.
  - 음의 경우에서 gradient가 죽는문제가 발생함.
  - 그래프의 모양이 zero-centered가 아님.
  - Learning rate를 신중하게 정해야함

* Leaky ReLU
  -  포화가 발생하지 않음.
  -  계산에 효율적임 (시간이 오래 걸리지않음).
  -  sigmoid, tanh 보다 수렴속도가 바름.
  -  gradient가 죽는 문제가 발생하지 않음.
  -  zero-mean에 가까운 출력
  
* ELU
  -  ReLU와 Leaky ReLU의 중간정도
  -  Saturation관점에서는 ReLU
  -  zero-centered의 괒넘에서는 Leaky ReLU와 닮아 있음


### Dead Relu 가 발생하는 경우
1. 초기화를 잘못한 경우
2. 가중치 평면이 data cloud에서 멀리 떨어져 있는 경우
3. learning rate 가 지나치게 큰 경우 (update를 지나치게 크게 해 가중치가 높아져 버리면 학습이 제대로 진행되지 않음)

## Data Preprocessing
* 데이터 전처리 (zero-mean) 을 하는이유
  - 모든 차원이 동일한 범위안에 있게 해줘서 전부 동등한 기여를 할 수 있게 함.
  - gradient 문제를 해결 할 수 있음.
  - 스케일이 다양한 ml 문제와 달리 이미지에서는 normalization을 엄청 잘 해줄 필요는 없음.
  - test 데이터에서도 train 데이터와 마찬가지로 zero-mean을 적용시켜줘야함
  - test 데이터에 적용하는 값은 train 데이 터의 전체 평균값임
  - mini-batch 단위로 학습하는 경우에도 zero-mean 처리는 train데이터의 전체 평균을 사용함

## Weight Initialization

### 모든 가중치를 동일하게(w = 0) 초기화 하면 발생하는 문제점
1. 출력이 모두 같다.
2. gradient가 모두 같다.
3. 모든 가중치가 같은 값으로 업데이트 된다.

### 초기화 문제를 해결하는 방법
1. 임의의 작은 값으로 초기화 (깊은 네트워크에서는 여전히 문제) w가 너무 작은 값들이어서 출력 값이 급격하게 줄어들음.
2. 가중치 초기화 값이 너무작으면 사라져버리고 너무 크면 saturation 문제가 발생함
3. activation 함수가 linear 하다는 가정하에 Xavier initialization 기법을 사용 할 수 있음

### ReLU 함수에서 Xavier initialization을 사용할 경우의 문제점
1. 출력의 분산을 반토막 내어버림

## Batch Normalization
guassian의 범위로 activation을 유지시키는 것에 관련한 아이디어

   * activaton function 의 입력값을 그래프에서 linear 한 영역에 위치하도록 강제하는 것.
   * saturation이 어느정도 일어나게 하고 싶으면 batch normalization을 할때 사용한 분산과 평균 값으로 x값을 원상복귀 시켜줄 수 있음
   * 각 레이어의 출력이 해당 데이터 하나 뿐만 아니라 batch 안에 존재하는 모든 데이터들에 영향을 받기 때문에 regularization 의 역할도 해줌

## Babysitting the Learning Process
1. 데이터 전처리
2. 모델 설계
3. loss 값 확인
4. train 마다 loss 값이 감소하는지 확인
5. 적절한 learning rate 찾기 보통 (1e-3 ~ 1e-5) 의 값을 사용

## Hyperparameter Optimization
### cross validation
- Training set으로 학습시키고 Validation set으로 평가하는 방법.
- 적은 에폭만으로도 어떤 parameter가 잘 동작하는지 확인 할 수 있음.
- 어느정도 parameter를 설정했다면 큰 에폭을 사용하고 fine search 를 수행함.
- 현재 cost 가 이전 cost 보다 비정상적으로 높아지면 학습이 잘못 수행되고있다는 증거.
- learning rate 값을 샘플링 할 때 10의 차수값만 샘플링하는것이 좋음 (learning rate는 그래디언트와 곱해지기 때문에 log scale을 사용하는 편이 더 좋음)

### Random search vs Grid search
- Random search 는 중요한 파라미터 에게도 더 많은 샘플링이 가능하므로 grid search보다 더 좋음.
  
  

