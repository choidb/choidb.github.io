---
title: '모델선택(Model Selection)'
use_math: true
categories:
  - ml
---



**목차**  
[1. 교차검증](#1-교차검증cross-validation)  
[2. 하이퍼파라미터 튜닝](#2-하이퍼파라미터-튜닝)  



---
* Contents
1. 교차검증
2. 하이퍼파라미터 최적화

---

## 1. 교차검증(Cross-validation)
* hold-out 교차검증의 문제점
  * 학습에 사용가능한 데이터가 충분하다면 문제가 없겠지만, 훈련세트의 크기가 모델학습에 충분하지 않을 경우 문제가 될 수 있습니다.
  * 검증세트 크기가 충분히 크지 않다면 예측 성능에 대한 추정이 부정확할 것입니다.
  * 등등..
  * 우리 문제를 풀기위해 어떤 학습 모델을 사용해야 할 것인지?
  * 어떤 하이퍼파라미터를 사용할 것인지?
    * &rArr; 모델선택(Model selection) 문제
    * 데이터의 크기에 대한 문제, 모델선택에 대한 문제를 해결하기 위해 사용하는 방법 중 한 가지가 **"교차검증(k-fold cross-validation(CV))"**이다.
      * 참고:교차검증은 시계열(time series) 데이터에는 적합하지 않습니다

* 교차검증(k-fold cross-validation(CV))
  * k개의 집합에서 k-1 개의 부분집합을 훈련에 사용하고 나머지 부분집합을 테스트 데이터로 검증함
  * 사이킷런에 cross_val_score 사용

## 2. 하이퍼파라미터 튜닝
* 하이퍼파라미터를 최적화 
  * 최적화는 훈련 데이터로 더 좋은 성능을 얻기 위해 모델을 조정하는 과정이다.
  * 일반화는 학습된 모델이 처음 본 데이터에서 얼마나 좋은 성능을 내는지를 말함
* 모델의 복잡도를 높이는 과정에서 훈련/검증 세트의 손실이 함께 감소하는 시점은 과소적합(underfitting) 되었다고 한다.
* 어느 시점부터 훈련데이터의 손실은 계속 감소하는데 검증데이터의 손실은 증가하는 때가 있는데 이를 과적합(overfitting) 되었다고 한다.
* 이상적인 모델은 과소적합과 과적합 사이에 존재함

* 검증곡선(validation curve)
  * 검증곡선은 훈련/검증데이터에 대해 x,y로 나타낸 그래프
    - y축: 스코어 
    - x축: 하이퍼파라미터
  - Scikit-learn, validation curves 를 사용하면 다양한 하이퍼파라미터 값에 대해 훈련/검증 스코어 값의 변화를 확인가능

* Randomized Search CV:
  * 검증하려는 하이퍼파라미터들의 값 범위를 지정해주면 무작위로 값을 지정해 그 조합을 모두 검증
* GridSearchCV: 
  * 검증하고 싶은 하이퍼파라미터들의 수치를 정해주고 그 조합을 모두 검증합니다.

* 선형회귀, 랜덤포레스트 모델들의 튜닝 추천 하이퍼파라미터
  * Random Forest
    * class_weight (불균형(imbalanced) 클래스인 경우)
    * max_depth (너무 깊어지면 과적합)
    * n_estimators (적을경우 과소적합, 높을경우 긴 학습시간)
    * min_samples_leaf (과적합일경우 높임)
    * max_features (줄일 수록 다양한 트리생성)
  * Logistic Regression
    * C (Inverse of regularization strength)
    * class_weight (불균형 클래스인 경우)
    * penalty
  * Ridge / Lasso Regression
    * alpha
