# 9강

# 목차

1. [LeNet-5](#lenet-5)

2. [ZFNet](#zfnet)

3. [VGGNet](#vggnet)

4. [GoogLeNet](#googlenet)

5. [Resnet](#resnet)
## CNN Architectures

### LeNet-5
- 산업에 적용하여 성공한 최초의 CNN

### AlexNet
- LeNet의 깊은 버전
- conv -> pool -> norm -> conv
- Input Size(224 * 224 * 3)
- 실제입력은 227 * 227 * 3

### ZFNet
- AlexNet의 하이퍼파라미터를 조정한 모델


### VGGNet
- 필터의 사이즈를 줄여 좀 더 딥한 네트워크 구조를 설계
- 깊이가 3인 3 * 3 filter는 7 * 7 filter 하나와 같은 역할을 할 수 있음
- 레이어가 깊어지면 파라미터 개수도 줄어들고 non-linearity를 추가할 수 있음


### GoogLeNet
- Inception module 개념 사용
- 파라미터수를 줄이기 위해 FC 레이어가 없음
- 1 * 1 conv(bottle neck layer)를 사용해 depth의 차원을 줄여줌
- Axiliary classifier를 사용하여 레이어가 깊어질수록 gradient값의 전파가 잘 안되는 문제점을 해결해줌

### Resnet
- 네트워크의 깊이가 깊다고 무조건 성능이 향상되자 않는다는 아이디어에서 출발
- 모델이 깊어지면 깊어질수록 optimization이 어려운 문제점을 해결
- skip connection(identity)을 이용해 원본 데이터의 값을 가져와 원본데이터의 값과의 잔차를 학습함
- bottle neck 레이어를 사용함으로써 계산량을 줄여줌

