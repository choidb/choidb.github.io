---
title: 'Choose your ML problems'
use_math: true
categories:
  - ml
---

**목차**  
[1. 데이터 과학자 실무 프로세스](#1-데이터-과학자-실무-프로세스)  
[2. 정보의 누수(leakage)가 없는지 확인](#2-정보의-누수leakage가-없는지-확인)  



---
* Contents
1. 예측모델을 위한 타겟을 올바르게 선택
2. 테스트/학습 데이터 사이 or 타겟과 특성들간 일어나는 정보의 누출(leakage)을 피하기
3. 상황에 맞는 검증 지표(metrics)를 사용하기

---

## 1. 데이터 과학자 실무 프로세스
1. 비즈니스 문제
실무자들과 대화를 통해 문제를 발견
2. 데이터 문제
문제와 관련된 데이터를 발견
3. 데이터 문제 해결
데이터 처리, 시각화
머신러닝/통계
4. 비즈니스 문제 해결
데이터 문제 해결을 통해 실무자들과 함께 해결

* 지도학습(Supervised learning)에서는 예측할 타겟을 먼저 정함.
  * 테이블 형태의 데이터세트인 경우 어떤 특성을 예측타겟으로 할지 먼저 정해야 한다.
* 회귀/분류문제가 쉽게 구분이 안되는 경우
  * 이산형, 순서형, 범주형 타겟 특성도 회귀문제 또는 다중클래스분류 문제로도 볼 수 있음
  * 회귀, 다중클래스분류 문제들도 이진분류 문제로 바꿀 수 있음.

## 2. 정보의 누수(leakage)가 없는지 확인
* 정보의 누수가 일어나 과적합을 일으키고 실제 테스트 데이터에서 성능이 급격하게 떨어지는 결과를 확인할 수 있음.
  * 타겟변수 외에 예측 시점에 사용할 수 없는 데이터가 포함되어 학습이 이루어 질 경우
  * 훈련데이터와 검증데이터를 완전히 분리하지 못했을 경우
* 불균형 클래스
  * 타겟 특성의 클래스 비율이 차이가 많이 날 경우가 많음
  * 대부분 scikit-learn 분류기들은 class_weight 와 같은 클래스의 밸런스를 맞추는 파라미터를 가지고 있음
  * 데이터가 적은 범주 데이터의 손실을 계산할 때 가중치를 더 곱하여 데이터의 균형을 맞추거나
  * 적은 범주 데이터를 추가샘플링(oversampling)하거나 반대로 많은 범주 데이터를 적게 샘플링(undersampling)하는 방법이 있음
  * [Handling Imbalanced Datasets in Deep Learning](https://towardsdatascience.com/handling-imbalanced-datasets-in-deep-learning-f48407a0e758)
* 회귀문제에서는 타겟의 분포를 주의깊게 보기
  * 선형 회귀 모델은 일반적으로 특성과 타겟간에 선형관계를 가정합니다.
  * 그리고 특성 변수들과 타겟변수의 분포가 정규분포 형태일때 좋은 성능을 보입니다.
  * 타겟변수가 왜곡된 형태의 분포(skewed)일 경우 예측 성능에 부정적인 영향을 미칩니다.
* 이상치 제거
  * 이상치가 포함되어 있다면 
* 로그변환(Log-Transform)
  * 타겟이 right-skewed 상태라면 로그변환을 사용하면 비대칭 분포형태를 정규분포형태로 변환시킴