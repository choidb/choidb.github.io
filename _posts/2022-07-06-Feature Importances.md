---
title: 'Feature Importances'
use_math: true
categories:
  - ml
---

**목차**  
[1. 모델 해석과 특성 선택을 위한 순열 중요도(Permutation Importances) 계산](#1-모델-해석과-특성-선택을-위한-순열-중요도permutation-importances-계산)  
[2. Boosting(xgboost for gradient boosting)를 사용](#2-boostingxgboost-for-gradient-boosting를-사용)  
[3. 그래디언트 부스팅](#3-그래디언트-부스팅)  
[4. 하이퍼파라미터 튜닝](#4-하이퍼파라미터-튜닝)  

---
* Contents
1. 특성 중요도 계산 방법들(permutation importances, Feature importance, ...)을 이해
2. gradient boosting
3. xgboost를 사용

---

## 1. 모델 해석과 특성 선택을 위한 순열 중요도(Permutation Importances) 계산
* 기본 특성 중요도는 빠르지만 특성 종류에 따라 부정확한 결과가 나올 수 있어 주의가 필요합니다.
* 순열 중요도 사용하면 더욱 정확한 계산이 가능합니다.

* 3가지 특성 중요도 계산 방법
1. Feature Importances(Mean decrease impurity, MDI)
* sklearn 트리 기반 분류기에서 디폴트로 사용되는 특성 중요도는 속도는 빠르지만 결과를 주의해서 봐야 합니다. 
* 각각 특성을 모든 트리에 대해 평균불순도감소(mean decrease impurity)를 계산한 값입니다.
* [Sklearn, DecisionTreeClassifier, min_impurity_decrease](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn-tree-decisiontreeclassifier)
* 불순도 감소(impurity decrease) 계산
  * $\displaystyle \frac{N_t}{N}$ * (impurity - $\displaystyle\frac{N_{tR}}{N_t}$ * right_impurity
                    - $\displaystyle\frac{N_{tL}}{N_t}$ * left_impurity)
  * $N$: 전체 관측치 수, $N_t$: 현재 노드 t에 존재하는 관측치 수

  * $N_{tL}$, $N_{tR}$: 노드 t 왼쪽(L)/오른쪽(R) 자식노드에 존재하는 관측치 수

  * 만약 `sample_weight`가 주어진다면, $N$, $N_t$, $N_{tR}$, $N_{tL}$는 가중합을 합니다.
* 특성 중요도가 높게 나온 state는 유의해서 봐야한다.
* 다른 특성과 비교하여 상대적으로 high-cardinarity 특성이라면 트리 구성 중 분기에 이용될 확률이 높아 과적합 위험이 있다.

2. Drop-Column Importance
* 이론적으로 가장 좋아 보이는 방법이지만, 매 특성을 drop한 후 fit을 다시 해야 하기 때문에 매우 느리다
* 특성이 n개 존재할 때 n + 1 번 학습이 필요함

3. 순열중요도, (Permutation Importance, Mean Decrease Accuracy,MDA)
* 기본 특성 중요도와 Drop-column 중요도 중간에 위치하는 특징을 가진다
* 중요도 측정은 관심있는 특성에만 무작위로 노이즈를 주고 예측을 하였을 때 성능 평가지표(정확도, F1, $R^2$ 등)가 얼마나 감소하는지를 측정한다.
* 순열중요도는 검증데이터에서 각 특성을 제거하지 않고 특성값에 무작위로 노이즈를 주어 기존 정보를 제거하여 특성이 기존에 하던 역할을 하지 못하게 하고 성능을 측정합니다. 이때 노이즈를 주는 가장 간단한 방법이 그 특성값들을 샘플들 내에서 섞는 것(shuffle, permutation) 입니다.
* eli5 라이브러를 사용해서 순열 중요도를 계산하기 참고 사이트
  * [The ELI5 library documentation explains, permutation importance](https://eli5.readthedocs.io/en/latest/blackbox/permutation_importance.html)
  - [eli5.sklearn.PermutationImportance](https://eli5.readthedocs.io/en/latest/autodocs/sklearn.html#eli5.sklearn.permutation_importance.PermutationImportance)
  - [eli5.show_weights](https://eli5.readthedocs.io/en/latest/autodocs/eli5.html#eli5.show_weights)
  - [scikit-learn user guide, `scoring` parameter](https://scikit-learn.org/stable/modules/model_evaluation.html#the-scoring-parameter-defining-model-evaluation-rules)

## 2. Boosting(xgboost for gradient boosting)를 사용
* 분류문제를 풀기 위해서는 트리 앙상블 모델을 많이 사용함
  * 트리 앙상블은 랜덤포레스트나 그래디언트 부스팅 모델을 이야기 하며 여러 문제에서 좋은 성능을 보이는 것을 확인하였습니다.
  * 트리모델은 non-linear, non-monotonic 관계, 특성간 상호작용이 존재하는 데이터 학습에 적용하기 좋습니다.
  * 한 트리를 깊게 학습시키면 과적합을 일으키기 쉽기 때문에. 배깅(Bagging, 랜덤포레스트)이나 부스팅(Boosting) 앙상블 모델을 사용해 과적합을 피합니다.
  * 랜덤포레스트의 장점은 하이퍼파라미터에 상대적으로 덜 민감한 것인데, 그래디언트 부스팅의 경우 하이퍼파라미터 셋팅에 따라 랜덤포레스트 보다 더 좋은 예측 성능을 보여줄 수도 있습니다.
* 부스팅과 배깅의 차이점은?
  * 랜덤포레스트의 경우 각 트리를 독립적으로 만들지만 부스팅은 만들어지는 트리가 이전에 만들어진 트리에 영향을 받는다
  * 부스팅 알고리즘 중 AdaBoost는 각 트리(약한 학습기들, weak learners)가 만들어질 때 잘못 분류되는 관측치에 가중치를 준다.
  * 다음 트리가 만들어질 때 이전에 잘못 분류된 관측치가 더 많이 샘플링되게 하여 그 관측치를 분류하는데 더 초점을 맞춘다.
* AdaBoost의 알고리즘
  * [AdaBoost 알고리즘 개념](https://dohk.tistory.com/217) 참고

<img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images2/2022-06-24-12-15-51.png?raw=true" width="400" height="100"/>

* $H(x)$ = 최종 강한 분류기 (Strong Classifier)이며, 약한 학습기들( ht )의 가중( α )합으로 계산
* $h$ = 약한 분류기 (Weak Classifier)
* $a$ = 약한 분류기의 가중치 (Weight)
* $T$ = 반복 횟수 (iteration)
* 여기서 $\alpha_t$ 가 크면 $e_t$가 작다는 것으로 분류기 $h_t$ 성능이 좋다는 것이고
여기서 $\alpha_t$ 가 작으면 $e_t$가 크다는 것으로 분류기 $h_t$ 성능이 안좋다는 뜻입니다.

## 3. 그래디언트 부스팅
* 그래디언트 부스팅은 회귀와 분류문제에 모두 사용가능
* 그래디언트 부스팅은 AdaBoost와 유사하지만 비용함수(Loss function)을 최적화하는 방법에 있어서 차이가 있다. 
* 그래디언트 부스팅에서는 샘플의 가중치를 조정하는 대신 잔차(residual)을 학습하도록 한다.
* 이것은 잔차가 더 큰 데이터를 더 학습하도록 만드는 효과가 있다.

#### sklearn 외에 부스팅이 구현된 여러가지 라이브러리
#### Python libraries for Gradient Boosting
- [scikit-learn Gradient Tree Boosting](https://scikit-learn.org/stable/modules/ensemble.html#gradient-boosting) — 상대적으로 속도가 느릴 수 있습니다.
  - Anaconda: already installed
  - Google Colab: already installed
- [xgboost](https://xgboost.readthedocs.io/en/latest/) — 결측값을 수용하며, [monotonic constraints](https://xiaoxiaowang87.github.io/monotonicity_constraint/)를 강제할 수 있습니다.
  - Anaconda, Mac/Linux: `conda install -c conda-forge xgboost`
  - Windows: `conda install -c anaconda py-xgboost`
  - Google Colab: already installed
- [LightGBM](https://lightgbm.readthedocs.io/en/latest/) — 결측값을 수용하며, [monotonic constraints](https://blog.datadive.net/monotonicity-constraints-in-machine-learning/)를 강제할 수 있습니다.
  - Anaconda: `conda install -c conda-forge lightgbm`
  - Google Colab: already installed
- [CatBoost](https://catboost.ai/) — 결측값을 수용하며, [categorical features](https://catboost.ai/docs/concepts/algorithm-main-stages_cat-to-numberic.html)를 전처리 없이 사용할 수 있습니다.
  - Anaconda: `conda install -c conda-forge catboost`
  - Google Colab: `pip install catboost`

* sklearn이 아닌 다른 라이브러리의 ML 모델
[XGBoost Python API Reference: Scikit-Learn API](https://xgboost.readthedocs.io/en/latest/python/python_api.html#module-xgboost.sklearn)
  * xgboost 는 랜덤포레스트보다 하이퍼파라미터 셋팅에 민감하다.
  * Early Stopping을 사용하여 과적합을 피할 수 있다.
    * Early Stopping 사용이유
      * GridSearchCV나 반복문을 사용하면 무려 `sum(range(1,n_rounds+1))` 트리를 학습해야 하며  `max_depth`, `learning_rate` 등등 파라미터 값에 따라 더 돌려야 되기 떄문
  - [Avoid Overfitting By Early Stopping With XGBoost In Python](https://machinelearningmastery.com/avoid-overfitting-by-early-stopping-with-xgboost-in-python/)

## 4. 하이퍼파라미터 튜닝
* Random Forest
  * max_depth (높은값에서 감소시키며 튜닝, 너무 깊어지면 과적합)
  * n_estimators (적을경우 과소적합, 높을경우 긴 학습시간)
  * min_samples_leaf (과적합일경우 높임)
  * max_features (줄일 수록 다양한 트리생성, 높이면 같은 특성을 사용하는 트리가 많아져 다양성이 감소)
  * class_weight (imbalanced 클래스인 경우 시도)
* XGBoost
  * learning_rate (높을경우 과적합 위험이 있습니다)
  * max_depth (낮은값에서 증가시키며 튜닝, 너무 깊어지면 과적합위험, -1 설정시 제한 없이 분기, 특성이 많을 수록 깊게 설정)
  * n_estimators (너무 크게 주면 긴 학습시간, early_stopping_rounds와 같이 사용)
  * scale_pos_weight (imbalanced 문제인 경우 적용시도)

[Notes on Parameter Tuning](https://xgboost.readthedocs.io/en/latest/tutorials/param_tuning.html) 참고
