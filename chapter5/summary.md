# 5강

# 목차

1. [Fully Connected Layer](#fully-connected-layer)

2. [Convolutional Layer](#convolutional-layer)

3. [Pooling](#pooling)

## Fully Connected Layer
- N * N * D 이미지를 (N*N*D)*1 형식으로 만듦
- 기존 이미지의 기하학적구조를 유지 하지 않음

## Convolutional Layer
- N * N * D 이미지의 shape를 보존한채 입력값으로 사용
- F * F 크기의 필터를 element-wise(아마다르 곱)곱으로 컨볼루션 연산을 수행
- 필터는 항상 원본이미지의 D 차원을 가지고 있음 즉 F * F * D
- output activation map 의 shape 는 (N - F) / S + 1임 ((N - F) % S == 0)
- 보통 CNN 에서 여러개의 특징을 추출하기 위해 N 개의 filter를 사용함.
- 보통 filter의 개수는 2의 제곱수로 정해줌.
- 뎁스의 차원을 줄여주는 목적으로 1*1 conv 연산도 수행함.
- 특정 컨볼루션 연산의 파라미터 수는 bias 고려한 (filtersize + 1) * filter_num 임

### Activation map
- 각 activation map 을 보고 특정 필터가 어떤 부분을 활성화 시켰는지 알 수 있음.
- 레이어가 깊어지면 깊어질수록 더 복잡한 특징을 보여줌 low-level -> mid-level -> high-level

### Zero-padding
- 모서리 부분의 값들을 컨볼루션 연산에 여러번 적용시킬수있도록 입력 map 의 크기를 늘려줌
- 아웃풋 activation map이 입력 map 의 크기를 유지할 수 있도록 해줌.

## Pooling
- 모델의 파라미터 개수를 줄여주기 위해 사용.
- pooling은 입력 맵의 depth에는 영향을 주지 않음.
- 일반적으로 stride를 맵의 값이 겹치지 않게 설정함.
- 특정 그리드 셀의 최대 활성화 정도를 보기 위해 average pooling 보다 max pooling 을 이용함




