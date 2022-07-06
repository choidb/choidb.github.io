# 신경망 학습(Training Neural Network)

**목차**  
[1. 신경망이 학습되는 메커니즘](#1-신경망이-학습되는-메커니즘)  
[2. 경사하강법(Gradient Descent)](#2-경사하강법gradient-descent)  
[3. 옵티마이저(Optimizer)](#3-옵티마이저optimizer)  


---
* Contents
1. 신경망이 학습되는 메커니즘(순전파, 손실 계산, 역전파)
2. 경사 하강법(Gradient Descent, GD)
3. 옵티마이저(Optimizer)
4. 확률적 경사 하강법(Stochastic Gradient Descent, SGD) 및 미니 배치 경사 하강법
5. 편미분(Partial Derivatives)과 연쇄 법칙(Chain Rule)


---

## 1. 신경망이 학습되는 메커니즘
1. 데이터가 입력되면 신경망 각 층에서 가중치 및 활성화 함수 연산을 반복적으로 수행합니다.
2. 1의 과정을 모든 층에서 반복한 후에 출력층에서 계산된 값을 출력합니다.
3. 손실 함수를 사용하여 예측값(Prediction)과 실제값(Target)의 차이를 계산합니다.
4. 경사하강법과 역전파를 통해서 각 가중치를 갱신합니다.
5. 학습 중지 기준을 만족할 때까지 1-4의 과정을 반복합니다.

* 1-4의 과정을 Iteration(이터레이션)이라고 하며 매 Iteration 마다 가중치가 갱신됨
* Iteration 은 순전파(1&2), 손실 계산(3), 역전파(4)로 나뉨
* 순전파(Forward Propagation)
  * 입력층에서 입력된 신호가 은닉층의 연산을 거쳐 출력층에서 값을 내보내는 과정
  * 연산과정
    * 입력층(혹은 이전 은닉층)으로부터 신호를 전달받습니다.
    * 입력된 데이터에 가중치-편향 연산을 수행합니다.
    * 가중합을 통해 구해진 값은 활성화 함수를 통해 다음 층으로 전달됩니다.
* 손실 함수(Loss function)
  * 입력 데이터를 신경망에 넣어 순전파를 거치면 마지막에는 출력층을 통과한 값이 도출되고 이 때 출력된 값과 그 데이터의 타겟값을 손실 함수에 넣어 손실(Loss or Error)를 계산함
  * 대표적인 손실 함수
    * MSE(Mean-Squared Error)
    * CEE(Cross-Entropy Error)
* 역전파(Backward Propagation)
  * 반대 방향으로 손실(Loss or Error) 정보를 전달해주는 과정
  * 손실 정보를 출력층부터 입력층까지 전달하여 각 가중치를 얼마나 업데이트 해야할 지를 구하는 알고리즘
  * 신경망은 매 반복마다 손실(Loss)을 줄이는 방향으로 가중치를 업데이트한다.
  * 손실을 줄이기 위해서 가중치 수정 방향을 결정하는 것이 바로 경사 하강법(Gradient Descent, GD)이다.

## 2. 경사하강법(Gradient Descent)
* **손실 함수 $J$ 의 경사(Gradient)가 작아지는 방향으로 업데이트** 하면 손실 함수의 값을 줄일 수 있음.
* 매 Iteration 마다 해당 가중치에서의 비용 함수의 도함수(=비용 함수를 미분한 함수)를 계산하여 경사가 작아질 수 있도록 가중치를 변경한다.
* 각 가중치가 갱신될 때 역전파의 주요 메커니즘인 편미분과 Chain rule(연쇄 법칙)이 사용된다.
* 특정 가중치  (θi)  에 대한 기울기는 아래 식과 같이 손실 함수를 해당 가중치로 편미분하여 구할 수 있음
  * $\frac{\partial}{\partial \theta_i} J(\theta)$
  * 모든 가중치에 대한 값은??
    * Chain rule이 적용
    * $\frac{\partial J(\theta)}{\partial \theta_i} = \frac{\partial J(\theta)}{\partial \theta_x} \cdot \frac{\partial \theta_x}{\partial \theta_i} = \frac{\partial J(\theta)}{\partial \theta_x} \cdot \frac{\partial \theta_x}{\partial \theta_y} \cdot \frac{\partial \theta_y}{\partial \theta_i}$

## 3. 옵티마이저(Optimizer)
* 경사를 내려가는 방법을 결정함
* 확률적 경사 하강법(Stochastic Gradient Descent, SGD)
  * 전체 데이터에서 하나의 데이터를 뽑아서 신경망에 입력한 후 손실을 계산
  * 손실 정보를 역전파하여 신경망의 가중치를 업데이트
  * Iteration 마다 1개의 데이터만을 사용
  * 장점: 가중치를 빠르게 업데이트 할 수 있다
  * 단점: 1개의 데이터만 보기 때문에 학습 과정에서 불안정한 경사 하강을 보인다
* 미니 배치(Mini-batch) 경사 하강법
  * N개의 데이터로 미니 배치를 구성하여 해당 미니 배치를 신경망에 입력한 후 이 결과를 바탕으로 가중치를 업데이트
  * Iteration 마다 N개(=배치 사이즈)의 데이터를 사용
    * 배치 사이즈(Batch Size)
      * 미니 배치 경사 하강법에서 사용하는 미니 배치의 크기
      * 2의 배수로 설정
      * 메모리 크기가 허락한다면 큰 배치 사이즈를 쓰는 것이 학습을 안정적으로 진행할 수 있음
      * 배치 사이즈가 작을 때
        * 경사 하강법을 통한 가중치 갱신이 불안정하여 최적점에 이르기까지 많은 Iteration 을 필요로 한다는 단점
    * 배치 사이즈가 클 때
      * 경사 하강법 과정에서 가중치 갱신이 안정적으로 일어나기 때문에 학습 속도가 빨라집니다.
      * 배치 사이즈를 너무 크게 설정하면 메모리를 초과해버리는 Out-of-Memory 문제가 발생
    * 최적의 배치 사이즈는?
      * 하이퍼파라미터 조정(Hyperparameter Tuning)
    * Data의 수, Epoch, 배치 사이즈, iteration의 관계
      * Data의 수 = Batch_size × Iteration