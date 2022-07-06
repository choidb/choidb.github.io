---
title: '결정트리(Decision Trees)'
use_math: true
categories:
  - ml
---

**목차**  
[1. 사이킷런 파이프라인](#1-사이킷런-파이프라인)  
[2. 결정트리](#2-결정트리)  
[3. 결정트리 학습 알고리즘](#3-결정트리-학습-알고리즘)  
[4. 과적합 해결](#4-과적합-해결)  
[5. 특성중요도](#5-특성중요도feature-importance)  
[6. 특성상호작용](#6-특성상호작용)  


---
* Contents
1. 파이프라인(pipelines)
2. 결정트리(decision tree)
3. 특성 중요도(feature importances)

* 사용하는 주요 라이브러리
  * category_encoders  
  * graphviz  
  * numpy  
  * pandas  
  * scikit-learn  

---

* cardinality 확인법
  * ~.describe(exclude='number')

## 1. 사이킷런 파이프라인
[Pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html) 참고
* ML 모델을 같은 전처리 프로세스에 연결
  * 결측치 처리, 스케일링, 모델학습 등 머신러닝 프로세스에서 파이프라인(Pipelines)을 사용하면 중복 코드를 최소화여 쉽게 연결 가능
  * 그리드서치(grid search)를 통해 여러 하이퍼파라미터를 쉽게 연결함.

## 2. 결정트리
[결정트리](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/) 참고
* 데이터를 분할해 가는 알고리즘
  * 결정트리(의사결정나무) 모델은 특성들을 기준으로 샘플을 분류해 나가는데 그 형태가 나무의 가지가 뻗어나가는 모습과 비슷함
  * 스무고개를 하는것과 비슷
  * 분류 과정은 새로운 데이터가 특정 말단 노드에 속한다는 정보를 확인한 뒤 말단노드의 빈도가 가장 높은 범주로 데이터를 분류
* 문이나 말단의 정답을 노드(node) 라 하며 노드를 연결하는 선을 엣지(edge)라 함
* 각 노드(node)는 뿌리(root)노드, 중간(internal)노드, 말단(external, leaf, terminal) 노드로 나뉨
* 결정트리는 분류와 회귀문제 모두 적용 가능
* 결정트리는 분류과정을 트리구조로 직관적으로 확인이 가능\

## 3. 결정트리 학습 알고리즘
* 결정트리를 학습하는 것은 노드를 어떻게 분할하는가에 대한 문제
* 결정트리의 비용함수를 정의하고 그것을 최소화 하도록 분할하는 것

**▪︎ 지니불순도(Gini Impurity or Gini Index):**

  * ${\displaystyle {I}_{G}(p) = \sum_{i=1}^{J} p_{i} (1-p_{i}) = 1-\sum_{i=1}^{J} {p_{i}}^{2}}$

**▪︎ 엔트로피(Entropy):**
  * ${\displaystyle \mathrm {H} (T)=\operatorname {I} _{E}\left(p_{1},p_{2},...,p_{J}\right)=-\sum_{i=1}^{J}{p_{i}\log_{2}p_{i}}}$

* 불순도(impurity) 라는 개념은 여러 범주가 섞여 있는 정도
  * 불순도가 낮은경우 지니불순도나 엔트로피는 낮은값 가짐
  * 노드를 분할하는 시점에서 가장 비용함수를 줄이는 분할특성과 분할지점을 찾아 내는 프로세스가 필요
  * 분할에 사용할 특성이나 분할지점(값)은 타겟변수를 가장 잘 구별해 주는(불순도의 감소가 최대가 되는, 정보획득이 가장 큰)것을 선택
  * 정보획득(Information Gain)은 특정한 특성을 사용해 분할했을 때 엔트로피의 감소량을 뜻함
  * ${\displaystyle IG(T,a)=\mathrm {H} {(T)}-\mathrm {H} {(T \vert a)}}$ = 분할전 노드 불순도 - 분할 후 자식노드 들의 불순도

* [sklearn.tree.DecisionTreeClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)

## 4. 과적합 해결
* 트리의 복잡도를 줄이기 위해 자주 사용하는 하이퍼파라미터들
  * min_samples_split
  * min_samples_leaf
  * max_depth

## 5. 특성중요도(feature importance)
* 회귀계수와 달리 특성중요도는 항상 양수값을 가진다.
* 이 값을 통해 특성이 얼마나 일찍 그리고 자주 사용되는지 결정된다.
* 결정트리모델은 선형모델과 달리 비선형, 비단조(non-monotonic), 특성상호작용(feature interactions) 특징을 가지고 있는 데이터 분석에 용의하다.
* 단조(Monotonic), 비단조(Non-monotonic) 함
* 특성상호작용
  * 특성들끼리 서로 상호작용을 하는 경우
  * 회귀분석에서는 서로 상호작용이 높은 특성들이 있으면 개별 계수를 해석하는데 어려움이 있고 학습이 올바르게 되지 않을 수 있다.
  * &rArr; 트리모델은 이런 상호작용을 자동으로 걸러내는 특징가짐

## 6. 특성상호작용
[Feature Interaction](https://christophm.github.io/interpretable-ml-book/interaction.html#feature-interaction) 참고
