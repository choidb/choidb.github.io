---
title: 'Logistic Regression'
use_math: true
categories:
  - ml
---

**목차**  
[1. 훈련/검증/테스트 세트 분리](#1-훈련검증테스트-세트-분리)  
[2. 분류 문제](#2-분류classification-문제)  
[3. 로지스틱 회귀](#3-로지스틱-회귀logistic-regression)  



---
* Contents
1. 훈련/검증/테스트(train/validate/test) 분리 이유
2. 분류와 회귀 문제의 차이
3. 로지스틱회귀

---

## 1. 훈련/검증/테스트 세트 분리
* 훈련세트로 모델을 한 번에 완전하게 학습시키기가 어려우며, 훈련세트로 튜닝된 여러 모델들을 학습한 후 어떤 모델이 학습이 잘 되었는지 검증하고 선택하는 과정이 필요하다.
* 훈련/검증세트로 좋은 모델을 만들어 낸 후 최종적으로 테스트세트에는 단 한번의 예측테스트를 진행을 한다.
  * 훈련데이터는 모델을 Fit 하는데 사용
  * 검증데이터는 예측 모델을 선택하기 위해서 예측의 오류를 측정할 때 사용
  * 테스트데이터는 일반화 오류를 평가하기 위해 선택된 모델에 한하여 마지막에 한 번 사용(훈련이나 검증과정에서 사용하지 않도록 주의)

## 2. 분류(Classification) 문제
* 다수 클래스를 기준모델로 정하는 방법(Majority class baseline)
  * 회귀문제에서는 보통 타겟 변수의 평균값을 기준모델로 사용
  * 분류문제에서는 보통 타겟 변수에서 가장 빈번하게 나타나는 범주를 기준모델로 설정
    * 분류문제 에서는 타겟 변수가 편중된 범주비율을 가지는 경우가 많음
    * 분류문제를 풀기전에 항상 먼저 타겟 범주가 어떤 비율을 가지고 있는지 확인해야 함.
  * 시계열(time-series) 데이터는 보통 어떤 시점을 기준으로 이전 시간의 데이터가 기준모델이 됨

* 분류 문제에서의 평가지표
  * 정확도(Accuracy): 분류문제에서 사용하는 평가지표
  * Accuracy = $\frac{올바르게 예측한 수}{전체 예측 수}$ = $\frac{TP + TN}{P + N}$

## 3. 로지스틱 회귀(Logistic Regression)
* 로지스틱회귀를 사용하면 타겟변수의 범주로 0과 1을 사용할 수 있으며 각 범주의 예측 확률값을 얻을 수 있다.
$\large P(X)={\frac {1}{1+e^{-(\beta _{0}+\beta _{1}X_{1}+\cdots +\beta _{p}X_{p})}}}$

$0 \leq P(X) \leq 1$
* 특성변수를 로지스틱 함수 형태로 표현
![](2022-06-23-21-49-01.png)
<img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images2/2022-06-23-21-49-01.png?raw=true" width="400" height="200"/>
* 분류문제에서는 확률값을 사용하여 분류를 하는데, 예를들어 확률값이 정해진 기준값 보다 크면 1 아니면 0 이라고 예측을 하게된다.

* Logit transformation
  * 로지스틱회귀의 계수는 비선형 함수 내에 있어서 직관적으로 해석하기가 어려운데 오즈(Odds) 를 사용하면 선형결합 형태로 변환 가능해 보다 쉽게 해석이 가능하다.
  * 오즈: 실패확률에 대한 성공확률의 비
  * $Odds = \large \frac{p}{1-p}$, 
    * p = 성공확률, 1-p = 실패확률
    * p = 1 일때 odds = $\infty$
    * p = 0 일때 odds = 0
    * $\large ln(Odds) = ln(\frac{p}{1-p}) = ln(\frac{\frac {1}{1+e^{-(\beta _{0}+\beta _{1}X_{1}+\cdots +\beta _{p}X_{p})}}}{1 - \frac {1}{1+e^{-(\beta _{0}+\beta _{1}X_{1}+\cdots +\beta _{p}X_{p})}}}) = \normalsize \beta _{0}+\beta _{1}X_{1}+\cdots +\beta _{p}X_{p}$
    * 오즈에 로그를 취해 변환하는 것을 로짓변환(Logit transformation) 이라 함.
    * 비선형형태인 로지스틱함수형태를 선형형태로 만들어 회귀계수의 의미를 해석하기 쉽게 하는데, 특성 X의 증가에 따라 로짓(ln(odds))가 얼마나 증가(or감소)했다고 해석을 할 수 있다.
    * (odds 확률로 해석을 하려면 exp(계수) = k 를 계산해서 특성 1단위 증가당 odds 확률이 k배 증가한다고 해석)
    * 기존 로지스틱형태의 y 값은 0~1의 범위를 가졌다면 로짓은 -$\infty$ ~ $\infty$ 범위를 가지게 된다.