---
title: '선형회귀(Linear Regression)'
use_math: true
categories:
  - ml
---


**목차**  
[1. 기준모델](#1-기준모델baseline-model-설정)  
[2. 예측모델](#2-예측모델predictive-model)  
[3. 단순 선형 회귀](#3-simple-linear-regression-단순-선형-회귀)  
  


---
* Contents
  1. 선형회귀모델
  2. 지도학습
  3. 회귀모델에 기준모델 설정
  4. Scikit-learn 이용

---

## 1. 기준모델(Baseline Model) 설정
* 분류문제: 타겟의 최빈 클래스
* 회귀문제: 타겟의 평균값
* 시계열회귀문제: 이전 타임스탬프의 값

#### 
```python
## predict: 우리가 정한 기준모델인 평균으로 예측을 합니다
predict = df['SalePrice'].mean()
## 평균값으로 예측할 때 샘플 별 평균값과의 차이(error)를 저장합니다
errors = predict - df['SalePrice']
## mean_absolute_error(MAE), error에 절대값을 취한 후 평균을 계산합니다.
mean_absolute_error = errors.abs().mean()
```

Mean Absolute Error(MAE, 평균절대오차) 는 예측 error 의 절대값 평균을 나타낸다.

* $Error = (price - guess)$

* $mae = (\frac{1}{n})\sum_{i=1}^{n}\left \vert price_{i} - guess_{i} \right \vert$

## 2. 예측모델(Predictive Model)

* 회귀분석에서 중요한 개념은 **예측값**과 **잔차(residual)** 이다.
  * 예측값은 만들어진 모델이 추정하는 값
  * 잔차는 예측값과 관측값 차이
    * (오차(error)는 모집단에서의 예측값과 관측값 차이를 말합니다.)

* 회귀선은 잔차 제곱들의 합인 RSS(residual sum of squares)를 최소화 하는 직선입니다. 
* RSS는 SSE(Sum of Square Error)라고도 말하며 이 값이 회귀모델의 비용함수(Cost function)가 됩니다. 
* 머신러닝에서는 이렇게 비용함수를 최소화 하는 모델을 찾는 과정을 학습이라고 합니다.

* ${\displaystyle \operatorname {RSS} =\sum_{i=1}^{n}(\varepsilon_{i})^{2}=\sum_{i=1}^{n}(y_{i}-f(x_{i}))^{2}=\sum_{i=1}^{n}(y_{i}-(\alpha x_{i} + \beta))^{2}}$

여기서 계수 $\alpha$ 와 $\beta$ 는 RSS를 최소화 하는 값으로 모델 학습을 통해서 얻어지는 값이다.

잔차제곱합을 최소화하는 방법을 최소제곱회귀 혹은 Ordinary least squares(OLS)라고 부른다.

OLS는 계수 계산을 위해 다음 공식을 사용한다.

* $\beta =\displaystyle {\bar {y}}-\alpha{\bar {x}}$,

* $\alpha ={\frac {S_{xy}}{S_{xx}}}$

* ${\displaystyle S_{xy}=\sum_{i=1}^{n}(x_{i}-{\bar {x}})(y_{i}-{\bar {y}})}$,   ${\displaystyle S_{xx}=\sum_{i=1}^{n}(x_{i}-{\bar {x}})^{2}}$

최소제곱법으로 선형 회귀계수를 구한다.

* 선형회귀는 주어져 있지 않은 점의 함수값을 보간(interpolate) 하여 예측하는데 도움을 줌.
* 기존 데이터의 범위를 넘어서는 값을 예측하기 위한 외삽(extrapolate)도 제공함.
  * 종속변수는 반응(Response)변수, 레이블(Label), 타겟(Target)등으로 불리며
  * 독립변수는 예측(Predictor)변수, 설명(Explanatory), 특성(feature) 등으로 불린다.

## 3. Simple Linear Regression (단순 선형 회귀)
[LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) 참고


* 선형회귀모델의 계수(Coefficients)

coef_:   
array of shape (n_features, ) or (n_targets, n_features)  
Estimated coefficients for the linear regression problem. If multiple targets are passed during the fit (y 2D), this is a 2D array of shape (n_targets, n_features), while if only one target is passed, this is a 1D array of length n_features.  

intercept_:  
float or array of shape (n_targets,)  
Independent term in the linear model. Set to 0.0 if fit_intercept = False.

