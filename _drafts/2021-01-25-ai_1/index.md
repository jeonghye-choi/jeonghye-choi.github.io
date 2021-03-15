---
title: 인공지능(AI)(1)
date: 2021-01-25
tags:
  - AI
keywords:
  - AI
---

# INDEX

## 인공지능

### 인공지능 구현하기

- 퍼셉트론
- 단층 퍼셉트론 (AND, OR)
- 다층 퍼셉트론 (XOR)

### 신경망

- 오차함수(MSE, 목적함수)
- Gradient Descent 학습법 (AND, OR)
- 오차역전파
- Optimizing
- Generalization
- 부작용(Vanishing Gradient/ Overfitting)
- 부작용 해결책(Dropout/ test set/ training set)
- Supervised Learning vs Non-supervised Learning

### 파이썬

- Numpy
- Pandas DataFrame
- 시각화(Matplotlib)

### Tensorflow

### Keras

### CNN

### DNN

### RNN

### LSTM

### GAN



<br/>
<br/>
<br/>

# 선행지식

## 수학지식

### 미분

### 3차원 그래프 (읽을 수 있는 정도)

### 선형대수 (행렬의 기본개념)


<br/>
<br/>
<br/>


# STUDY

## 인공지능

#### > 지능이란?

스스로 생각하면 지능이 있는 것일까?
그럼 생각은 뭘까?
외부의 자극에 반응하는 것?
그럼 외부의 자극에 반응하는 것이 지능인 것일까?
그렇다면 피아노나 플룻과 같은 악기도 지능이 있다고 말할 수 있을까?
놉!
어떤 원인에 대해서 복잡한 계산끝에 결론이 내려졌다고 해서 '지능'이 있다고 말할 수 없다.

만약 그림을 그린다고 해보자.
그리면 그릴 수록 점점 더 잘 그려진다.
즉, 완벽히 돼지를 그리는 것은 아닐지라도 점점 발전하고 있다. 점점 더 정답에 가까워지고 있다.
학습하고 있다.

즉, 지능은 스스로 학습하는 것을 말합니다.
외부 자극에 대한 반응이 아닌

외부 자극에 반응을 스스로 (점차 정답에 근접하게) 만드는 것



### 인공지능 구현하기

INPUT에 대해 스스로 점차 정답에 가까운 F(x)를 만드는 Function f 만들기
를 효율적으로/능률적으로 구현하는 방법?은 뭐가 있을까?

인간의 뇌(학습과정)을 흉내내는 것!

뉴런을 코드로 구현할 수 있다면 => Tensorflow

#### > 뉴런

주어진 자극을 모으고 -> 그 자극들을 처리해서 -> 가공한 결과를 내보낸다(다른 뉴런의 자극이 된다)

input 값을 모으고 -> 그 input 값을 처리해서 -> 가공한 결과를 내보낸다

input값을 모았을 때 일정이상의 값이 되어야 내보내는데 그 때 작동하는 함수가 Activation function이다.

- 퍼셉트론
  (사진1)

#### > Activation function

  f(net) = f(w0x0 + w1x1 + w2x2)
  net이 일정 이상보다 크면 그대로 내보내고, 아니면 내보내지 않는 함수f(net)
  net을 보고 최종적으로 output을 결정하는 함수f(net) = Activation Function

  (사진2)
  net이 임계값을 넘으면 발동하는 함수f(net)

  - Activation function의 종류 (사진3)
    - sigmoid
    - tanh
    - ReLU
    - Leaky ReLU
    - Maxout
    - ELU


#### > 퍼셉트론

- 단층 퍼셉트론 (AND, OR, NOT)

  그래프로 그렸을 때 값을 하나의 직선으로 구분할 수 있다.
  하지만 XOR의 경우 하나의 선으로는 부족한 것을 알 수 있다.

  => 선 하나로 분류할 수 있는 문제 = 선형 분류 문제
    선 하나로 분류할 수 없는 문제 = 비선형 분류 문제

- 그럼 어떻게 해결할 수 있을까?

  1. 직선의 개수를 늘린다. => "식이 하나 더 있으면 됨!"
  2. input의 차원을 늘린다. (하나의 직선으로는 linear 분리가 어렵지만, 하나의 평면으로는 linear 분리가 가능하다) (사진5)

  => 수식 두개 = 단층 퍼셉트론 두 개 = 다층 퍼셉트론!

- 다층 퍼셉트론 (XOR (둘다 다르면 1))

  (사진6)
  Input layer - Hidden layer - Output layer

  - 첫번째 layer역할 : input을 선형분리가 가능하도록 변경! (???첫번째 래에어는 inputlayer를 말하는 걸까?) (사진8)


  (사진7)
  여러개의 퍼셉트론이 연결되면 => Deep Neural networks


#### > 학습 방법

- Random initialization (사진9)
- Weights Adjustment



#### > 에러를 최소화 하는 방법 Minimize the errors

Error = 정답(target)과 system의 output f(x)와의 차이

제곱을 해서 오차를 평균내면 => 평균제곱오차(MSE) (.=.오차의 절댓값)

==> MSE(평균제곱오차)를 최소화시키는 방법(오차를 최소화 시키는 방법)


#### > 경사 하강법(Gradient Descent 학습법)

Error가 가장 작을 때의 weight를 찾는 것
(사진10)

1. weight의 값을 최초의 랜덤한 값으로 초기화.
2. Training마다, network는 이 weight를 에러가 줄어드는 방향으로 재조정
3. Error함수의 최소점이 될 때까지 재조정
4. Error 함수값을 최소로 만드는 w가 우리가 바라는 weight

- Learning Rate

  Weight 변화를 줄때 변화되는 정도
  (사진11)
  (사진12)

### 신경망

- 오차함수(MSE, 목적함수)
- Gradient Descent 학습법 (AND, OR)
- 오차역전파
- Optimizing
- Generalization
- 부작용(Vanishing Gradient/ Overfitting)
- 부작용 해결책(Dropout/ test set/ training set)
- Supervised Learning vs Non-supervised Learning

### 파이썬

- Numpy
- Pandas DataFrame
- 시각화(Matplotlib)

### Tensorflow

### Keras

### CNN

### DNN

### RNN

### LSTM

### GAN
