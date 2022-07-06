# Hyperparameters

**목차**  
[1. 하이퍼파라미터(Hyperparameter) 튜닝으로 성능 올리기](#1-하이퍼파라미터hyperparameter-튜닝으로-성능-올리기)  
[2. 실험 기록 툴(wandb 등)에 대해 알아보기](#2-실험-기록-툴wandb-등에-대해-알아보기)  


---
* Contents
1. 하이퍼파라미터 탐색법 중 Grid 탐색법과 Random 탐색법
2. Scikit-learn 와 Keras Tuner 를 사용한 신경망의 하이퍼파라미터 탐색
3. 신경망의 주요 용어
4. 실험 계획 라이브러리인 WandB

---

## 1. 하이퍼파라미터(Hyperparameter) 튜닝으로 성능 올리기
* 하이퍼파라미터 튜닝 방식의 종류
  1. "Babysitting"(육아) 혹은 "Grad Student Descent"(대학원생 갈아넣기)
       * 100% 수작업(Manual)으로 파라미터를 수정하는 방법
  2. Grid Search
       * 하이퍼파라미터마다 탐색할 지점을 정해주면 모든 지점에 해당하는 조합을 알아서 수행
       * 1개, 혹은 최대 2개 정도의 파라미터 최적값을 찾는 용도로 적합
  3. Random Search
       * 지정된 범위 내에서 무작위로 모델을 돌려본 후 최고 성능의 모델을 반환
       * 시도 횟수를 정해줄 수 있기 때문에 Grid Search 에 비해서 훨씬 적은 횟수로 수행
       * 상대적으로 중요한 하이퍼파라미터에 대해서는 탐색을 더 하고, 덜 중요한 하이퍼파라미터에 대해서는 실험을 덜 하도록 한다.
  4. Bayesian Methods
       * 이전 탐색 결과 정보를 새로운 탐색에 활용하는 방법
       * 베이지안 방법을 사용하면 하이퍼파라미터 탐색 효율을 높일 수 있음
       * bayes_opt 나 hyperopt와 같은 패키지를 사용하면 베이지안 방식을 적용할 수 있음
* 튜닝 가능한 파라미터
  * 배치 크기(batch_size)
  * 에포크(epochs)
  * 옵티마이저(optimizers)
  * 학습률(learning rate)
  * 활성화 함수(activation)
  * Regularization(weight decay, Dropout 등)
  * 은닉층(Hidden layer)의 노드(Node) 수

## 2. 실험 기록 툴(wandb 등)에 대해 알아보기
* 다양한 하이퍼파라미터를 변경해가면서 결과를 관리하기 위한 방법임
  * Comet.ml, Weights and Biases(wandb) 등 사용
  * 코드와 결과값을 보관
  * 실험 결과를 원하는 기준대로 언제든지 시각화하여 모델의 성능을 확인할 수 있도록 도와줌
  * 매 Epoch이 끝날 때마다 데이터가 해당 툴에 보내지기 때문에 모델이 수렴하고 있는지도 확인 가능

