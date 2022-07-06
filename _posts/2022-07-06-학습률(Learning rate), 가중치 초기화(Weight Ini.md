---
title: '학습률(Learning rate), 가중치 초기화(Weight Initialization) & Regularization'
use_math: true
categories:
  - dl
---

**목차**  
[1. 학습률 감소/계획법(Learning rate Decay/Scheduling)](#1-학습률-감소계획법learning-rate-decayscheduling)  
[2. 가중치 초기화(Weight Initialization)](#2-가중치-초기화weight-initialization)  
[3. 과적합(Overfitting)](#3-과적합overfitting)  
[4. 옵티마이저(Optimizer)](#4-옵티마이저optimizer)  


---
* Contents
1. 학습률
2. 가중치 초기화
3. 과적합 방지 방법
4. Dropout


---

## 1. 학습률 감소/계획법(Learning rate Decay/Scheduling)
* 학습률(Learning rate)
  *  매 가중치에 대해 구해진 기울기 값을 얼마나 경사 하강법에 적용할 지를 결정하는 하이퍼파라미터(얼마나 이동할 지를 조정하는 하이퍼파라미터)
  * 학습률이 너무 낮으면 최적점에 이르기까지 너무 오래 걸리거나, 주어진 Iteration 내에서 최적점에 도달하는 데 실패하기도 한다.
  * 학습률이 너무 높으면 경사 하강 과정에서 발산하면서 모델이 최적값을 찾을 수 없게 된다.
* 학습률 감소(Learning rate Decay)
  * Adagrad, RMSprop, Adam 과 같은 주요 옵티마이저에 이미 구현되어 있기 때문에 쉽게 적용 가능
  * .compile 내에 있는 optimizer= 에 Adam 등의 옵티마이저 적용 후 내부 하이퍼파라미터를 변경하면 학습률 감소를 적용할 수 있습니다.  

#### ex)
```python
model.compile(optimizer=tf.keras.optimizers.Adam(lr=0.001, beta_1 = 0.89)
             , loss='sparse_categorical_crossentropy'
             , metrics=['accuracy'])
```
* 학습률 계획법(Learning rate Scheduling)
  * .experimental 내부의 함수를 사용하여 설계

#### ex)
```python
first_decay_steps = 1000
initial_learning_rate = 0.01
lr_decayed_fn = (
  tf.keras.experimental.CosineDecayRestarts(
      initial_learning_rate,
      first_decay_steps))
model.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=lr_decayed_fn)
             , loss='sparse_categorical_crossentropy'
             , metrics=['accuracy'])
```

## 2. 가중치 초기화(Weight Initialization)
1. 표준편차를 1인 정규분포로 가중치를 초기화 할 때 각 층의 활성화 값 분포
   * 표준편차가 일정한 정규분포로 가중치를 초기화 해 줄 때에는 대부분의 활성화 값이 0과 1에 위치

2. Xavier 초기화를 해주었을 때의 활성화 값의 분포
   * Xavier 초기화(Xavier initialization)는 가중치를 표준편차가 고정값인 정규분포로 초기화 했을 때의 문제점을 해결하기 위해 등장한 방법
   * Xavier 초기화는 이전 층의 노드가 n 개일 때, 현재 층의 가중치를 표준편차가 $\frac{1}{\sqrt{n}}$ 인 정규분포로 초기화한다.
   * *(케라스에서 Xavier 초기화는 이전 층의 노드가 n 개이고 현재 층의 노드가 m 개일 때, 현재 층의 가중치를 표준편차가 $\frac{2}{\sqrt{n+m}}$ 인 정규분포로 초기화합니다.)*
   * Xavier 초기화는 활성화 함수가 시그모이드(Sigmoid)인 신경망에서는 잘 동작합니다.
   * 하지만 활성화 함수가 ReLU 일 경우에는 층이 지날수록 활성값이 고르지 못하게 되는 문제가 있음.

3. He 초기화를 해주었을 때의 활성화 값의 분포
   * 활성화 함수가 ReLU 일 경우에는 층이 지날수록 활성값이 고르지 못하게 되는 문제에 대한 해결로 나온 초기화 &rArr; He 초기화
   * 이전 층의 노드가 n 개일 때, 현재 층의 가중치를 표준편차가 $\frac{2}{\sqrt{n}}$ 인 정규분포로 초기화한다.
   * He 초기화를 적용하면 아래 그림처럼 층이 지나도 활성값이 고르게 유지됨

* 가중치 초기화 방법을 요약
  * Activation function에 따른 초기값 추천
    * Sigmoid ⇒ Xavier 초기화를 사용하는 것이 유리
    * ReLU ⇒ He 초기화 사용하는 것이 유리

## 3. 과적합(Overfitting)
* 과적합 방지를 위한 방법들
  1. Weight Decay (가중치 감소) 
     * 가중치가 너무 커지지 않도록 가중치 값이 너무 커지지 않도록 조건을 추가
     * 손실 함수(Cost function)에 가중치와 관련된 항을 추가
     * 조건을 어떻게 적용할지에 따라 L1 Regularization(LASSO), L2 Regularization(Ridge) 으로 나뉨
     * 각 방법에 따른 손실 함수 식
$$\begin{aligned}
L_1(\theta_w) &= \frac{1}{2} \sum_i (output_i - target_i)^2 + \color{blue}{\lambda} \cdot \color{red}{\Vert \theta_w \Vert_1}\\
L_2(\theta_w) &= \frac{1}{2} \sum_i (output_i - target_i)^2 + \color{blue}{\lambda} \cdot \color{red}{\Vert \theta_w \Vert_2}
\end{aligned}$$

* Keras 에서는 아래와 같이 가중치 감소를 적용하고 싶은 층에 `regularizer` 파라미터를 추가

  2. Dropout (드롭아웃)
     * Iteration 마다 레이어 노드 중 일부를 사용하지 않으면서 학습을 진행하는 방법
     * 매 번 다른 노드가 학습되면서 전체 가중치가 과적합되는 것을 방지
     * Dropout 을 적용할 때에는 0~1 사이의 실수를 입력
     * 모델 내에 있는 특정 레이어의 노드 연결을 지정해 준 비율만큼 강제로 끊음
     * 매 Iteration 마다 랜덤하게 노드를 차단하여 다른 가중치를 학습하도록 조정하기 때문에 과적합을 방지
     * Keras 에서는 아래와 같이 Dropout 을 적용하고 싶은 층 다음에 Dropout 함수를 추가하면됨

  3. Early Stopping (조기 종료)
     * 학습(Train) 데이터에 대한 손실은 계속 줄어들지만 검증(Validation) 데이터셋에 대한 손실은 증가한다면 학습을 종료하도록 설정하는 방법


## 4. 옵티마이저(Optimizer)
* Momentum(모멘텀)
  * Momentum 의 사전적 정의는 '운동량, 관성'
  * 옵티마이저에 관성을 부여하는 하이퍼파라미터
  * 기울기 변화가 심한 방향으로는 값을 더 많이 개선하게되고 기울기 변화가 완만한 방향으로는 값을 덜 개선하게 됩니다.
  * 지역 최적점(Local minima)에서 빠져 나올 수 있도록 해준다.
* Adagrad(아다그라드)(=Adaptive Gradient)
  * 자주 등장하는 특성의 파라미터에 대해서는 낮은 학습률을, 가끔 등장하는 특성의 파라미터에 대해서는 높은 학습률을 적용
  * 희소한 데이터에 대해 이 방법을 적용할 경우 훨씬 더 강건(Robust)하다는 장점이 있음
  * 학습률을 조정해주지 않아도 알아서 적절한 학습률을 적용한다
  * 학습이 진행될수록 Gt값이 커지고 학습률이 점점 줄어들게 되어 많은 반복 학습 이후에는 파라미터가 거의 갱신되지 않는 문제가 발생하기도 합니다.
* Adam(아담)
  * Adam(Adaptive moment estimation, 아담)은 Momentum 에 적용된 그래디언트 조정법과 Adagrad 에 적용된 학습률 조정법의 장점을 융합한 옵티마이저
