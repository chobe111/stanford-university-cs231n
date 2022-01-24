# 8강

# 목차
1. [CPU](#cpu)

2. [GPU](#gpu)

3. [Pytorch and Tensorflow](#pytorch-and-tensorflow)
4. 
## CPU
- 딥러닝에 관해서는 NVIDIA가 독점
- 보통 cpu는 한번에 20가지의 일(스레드)을 할 수 있음 
- gpu 코어의 수가 많다는 것은 어떤 task 를 병렬로 수행하기에 적합하다는 뜻임
- cpu는 대부분의 메모리를 RAM 에서 끌어다 씀 
- ram 과 gpu간의 통신은 상당한 bottle neck을 초래하기 때문에 보통 칩에 ram이 내장되어있음
- 행렬곱 연산은 gpu 에서 정말 잘 동작하고 아주 적합한 알고리즘임

## GPU
- GPU 코어의 수가 많다는 것은 어떤 task를 병렬로 수행하기에 적합하다는 뜻
- RAM과 GPU간의 통신은 상당한 bottle neck을 초래하기 때문에 보통 칩에 RAM이 내장되어있음
- 행렬곱(Matrix multiplication)연산은 GPU에서 정말 잘 동작하고 아주 적합한 알고리즘임
- 결과 행렬의 각 요소들을 병렬로 계산할 수 있음

### AMD vs NVIDIA
- 딥러닝에 관해서는 NVIDIA가 독점

## Pytorch and Tensorflow

### Static vs Dynamic
- static graphs 에는 그래프를 최적화시킬 수 있는 여지가 주어짐.

* Serialize
  - 그래프를 한번 구성하면 메모리에 저장하고 그래프 자체를 Disk 에 저장할 수 있음 즉 전체 네트워크 구조를 파일 형태로 저장 할 수 있음
  - 그래프의 구성과 그래프 실행 하는 과정이 얽혀있기 때문에 모델을 복구하려면 원본 코드가 있어야함 

* Conditional
  - Dynamic graph
    - 특정 함수 구문안에서 조건문을 단순히 추가해주기만 하면 됨
    - 그래프 내에 control flow를 넣어줘야함

* Loops
  - Dynamic graph (Pytorch)
    - 단순 for문을 사용하여 구현
  - Conditinal graph (Tensorflow)
    - 그래프에 명시적으로 loop를 넣어줘야만 함

* Dynamic Graph Applications
  - Recurrent networks
    - 입력 sequence 에 따라 computational graph가 더 커질 수도, 작아질 수도 있음   
  - Recursive networks
    - 기존의 파이썬 control flow 만 사용하여 구현 가능 
  - Modular Network 
    - 질문이 주어지면 그 질문에 맞는 그래프를 구성함