# Ridge Regression

**목차**  
[1. 원핫인코딩](#1-원핫인코딩)  
[2. 특성 선택](#2-특성-선택feature-selection)  
[3. Ridge regression 모델 학습](#3-ridge-regression-모델-학습)  
[4. OLS vs Ridge](#4-ols-vs-ridge)  


---
* Contents
1. 원핫인코딩
2. Ridge 회귀를 통한 특성 선택
3. 정규화를 위한 Ridge 회귀모델

---

## 1. 원핫인코딩
* 범주형 자료는 순서가 없는 명목형(nominal)과, 순서가 있는 순서형(ordinal)으로 나뉨
* 원핫인코딩을 수행하면 각 카테고리에 해당하는 변수들이 모두 차원에 더해지게 됩니다. 그러므로 카테고리가 너무 많은 경우(high cardinality)에는 사용하기 적합하지 않다.
  * get_dummies
  * Category_encoders 라이브러리 사용(범주형변수를 가진 특성만 원핫인코딩 수행)
    * OneHotEncoder

## 2. 특성 선택(Feature selection)
* 특성공학(feature engineering)
  * 과제에 적합한 특성을 만들어 내는 과정
  * 실무 현장에서 가장 많은 시간이 소요되는 작업 중 하나
* SelectKBest를 사용해 가장 효과적인 특성 K개를 고르기
```ipython
# target(Price)와 가장 correlated 된 features 를 k개 고르는 것이 목표입니다.

## f_regresison, SelectKBest
from sklearn.feature_selection import f_regression, SelectKBest

## selctor 정의합니다.
selector = SelectKBest(score_func=f_regression, k=10)

## 학습데이터에 fit_transform 
X_train_selected = selector.fit_transform(X_train, y_train)

## 테스트 데이터는 transform
X_test_selected = selector.transform(X_test)


X_train_selected.shape, X_test_selected.shape
```
* 특성의 수 k를 어떻게 결정하는가??

## 3. Ridge Regression 모델 학습
* Ridge 회귀는 기존 다중회귀선을 훈련데이터에 덜 적합이 되도록 만든다

$\beta_{ridge}$:  $argmin[\sum_{i=1}^n(y_i - \beta_0 - \beta_1x_{i1}-\dotsc-\beta_px_{ip})^2 + \lambda\sum_{j=1}^p\beta_j^2]$

* n: 샘플수, p: 특성수, $\lambda$: 튜닝 파라미터(패널티)
  * 참고: alpha, lambda, regularization parameter, penalty term 모두 같은 뜻

* Ridge 회귀는 **과적합을 줄이기 위해서** 사용
  * 과적합을 줄이는 간단한 방법 중 한 가지는 모델의 복잡도를 줄이는 것임.
  * 특성의 갯수를 줄이거나 모델을 단순한 모양으로 적합하는 것임.
  * Ridge 회귀는 이 **편향을 조금 더하고, 분산을 줄이는 방법**으로 정규화(Regularization)를 수행함.
  * 정규화는 모델을 변형하여 과적합을 완화해 일반화 성능을 높여주기 위한 기법임.
    * 정규화의 강도를 조절해주는 패널티값인 람다의 성질
      * $\lambda$ → 0,   $\beta_{ridge}$ → $\beta_{OLS}$
      * $\lambda$ → ∞,   $\beta_{ridge}$ → 0.

## 4. OLS vs Ridge
* OLS (Ordinary Least Squares, 최소자승법): 잔차제곱합(RSS: Residual Sum of Squares)를 최소화하는 가중치 벡터를 구하는 방법
* alpha = 0인 경우에는 OLS 와 같은 그래프 형태로 같은 모델 임을 확인 할 수 있고. alpha 값이 커질 수록 직선의 기울기가 0에 가까워 지면서 평균 기준모델(baseline) 과 비슷해진다.
* RidgeCV를 통한 최적 패널티(alpha, lambda) 검증
* 다수의 특성을 사용하는 다항함수에 Ridge 회귀를 사용하면 정규화 효과를 더 잘 확인가능
* RidgeCV를 사용하여 최적의 alpha값을 찾아내어 모델 학습을 진행한다.
* Ridge 회귀는 정규화를 통해 특이값으로 인한 과도한 기울기를 보정해 주며, 영향력이 낮은 특성의 회귀계수의 값을 감소시켜 특징선택 효과를 준다.
