# 2강

# 목차

1. [이미지 분류](#이미지-분류)

2. [한계점](#한계점)

3. [CNN 이전의 이미지 분류 방법](#cnn-이전의-이미지-분류-방법)

4. [Data driven approach](#data-driven-approach)

5. [Distance metric to compare images](#distance-metric-to-compare-images)

6. [Setting Hyperparameter](#setting-hyperparamter)

7. [KNN 알고리즘을 이미지에서 사용하지 않는 이유](#knn-알고리즘을-이미지에서-사용하지-않는-이유)

8. [Linear Classification](#linear-classification)


## 이미지 분류 
Image -> Classify -> Result (물체의 종류)
## 한계점
1. 카메라 각도의 변환: 각도의 변환이 이루어지면 이미지의 픽셀값이 전체적으로 달라짐
2. 조명 문제: 빛으로 인해 물체의 형상이 제대로 보이지 않을 경우 (illusion)
3. 물체의 변형: 물제의 pose가 일정하지 않을 경우 (deformation)
4. 폐색: 물체가 다른사물에 가려져 제대로 보이지 않을 경우
5. 배경과 물체가 제대로 구분이 안되는 경우 (background clutter)
6. 같은 종류 클래스의 다양성 (intraclass variation)

## CNN 이전의 이미지 분류 방법

Image -> Find Edge -> Find Corner -> Result

## Data driven approach
1. 데이터 수집
2. 수집한 데이터를 위한 분류기 개발
3. 테스트 셋에서의 검증

## Distance metric to compare images

### L1 (Manhattan) Distance

$$\left\lvert \displaystyle\sum_{p}{(I_1^P - I_2^P)} \right\rvert$$
* 좌표계에 따라 거리 값이 달라질 수 있음
* 각각의 벡터가 특징을 가지고 있을때 사용


### L2 (Euclidean) Distance

$$\left\lvert \displaystyle \sqrt{\sum_{p}{(I_1^P - I_2^P)}^2} \right\rvert$$
* 특정 벡터가 일반적이고 요소들간의 실질적인 의미를 잘 모를때 사용

## Setting Hyperparamter

1. Idea 1: 트레인 데이터에서 성능이 좋은 값 (x)
2. Idea 2: 학습과 테스트 셋으로 데이터를 나누어 테스트에서 잘 동작하는 값 (x)
3. Idea 3: train, test, validation 으로 나누어 학습 진행 (o)
4. Idea 4: cross validation (전체 학습데이터중 train 셋과 validation 셋을 바꿔가며 검증) [데이터셋이 적을때 사용] (o)


## KNN 알고리즘을 이미지에서 사용하지 않는 이유
* 매우느림 (인퍼런스)
* 픽셀 값 데이터는 이미지 정보를 충분하게 나타내지 못함

## Linear Classification

선을 이용해 집단을 두개 이상으로 구분함

Image -> $f(x,W)$ -> Label

$$f(x,W)=Wx + b $$

### 한계점
홀짝과 같은 반정성 문제는 Linear Classification 으로 풀기 힘든 문제임


