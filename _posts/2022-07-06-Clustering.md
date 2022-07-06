# Clustering

**목차**  
[1. Scree plots](#1-scree-plots)  
[2. Machine Learning](#2-machine-learning)  
[3. Clustering](#3-clustering)  
  


---
* Contents
  1. Screeplot
  2. Supervised / Unsupervised learning
  3. K-means clustering

---

## 1. Scree Plots
```ipython
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np
%matplotlib inline
from sklearn.datasets import make_blobs
from sklearn import decomposition

X1, Y1 = make_blobs(n_features = 10, n_samples = 100, centers = 4, random_state = 4, cluster_std = 2) ## random 하게 simulation data 생성

pca = decomposition.PCA(n_components = 4)
pc = pca.fit_transform(X1)

pc_df = pd.DataFrame(data = pc, columns = ['PC1', 'PC2', 'PC3', 'PC4'])
pc_df['Cluster'] = Y1
pc_df.head()

def scree_plot(pca):
    num_components = len(pca.explained_variance_ratio_)
    ind = np.arange(num_components)
    vals = pca.explained_variance_ratio_
    
    ax = plt.subplot()
    cumvals = np.cumsum(vals)
    ax.bar(ind, vals, color = ['#00da75', '#f1c40f',  '#ff6f15', '#3498db']) # Bar plot
    ax.plot(ind, cumvals, color = '#c0392b') # Line plot 
    
    for i in range(num_components):
        ax.annotate(r"%s" % ((str(vals[i]*100)[:3])), (ind[i], vals[i]), va = "bottom", ha = "center", fontsize = 13)
     
    ax.set_xlabel("PC")
    ax.set_ylabel("Variance")
    plt.title('Scree plot')
    
scree_plot(pca)
```

## 2. Machine Learning
* 지도 학습 (Supervised Learning): Supervised Learning은 트레이닝 데이터에 라벨(답)이 있을때 사용가능
  * 분류 (Classification) 분류 알고리즘은 주어진 데이터의 카테고리 혹은 클래스 예측을 위해 사용
  * 회귀 (Prediction) 회귀 알고리즘은 continuous 한 데이터를 바탕으로 결과를 예측 하기 위해 사용
* 비지도 학습 (Unsupervised Learning)
  * 클러스터링 (Clustering) 데이터의 연관된 feature를 바탕으로 유사한 그룹을 생성
  * 차원 축소 (Dimensionality Reduction 높은 차원을 갖는 데이터셋을 사용하여 feature selection / extraction 등을 통해 차원을 줄이는 방법
  * 연관 규칙 학습 (Association Rule Learning) 데이터셋의 feature들의 관계를 발견하는 방법
  * 강화 학습 (Reinforcement Learning) 머신러닝의 한 형태로, 기계가 좋은 행동에 대해서는 보상, 그렇지 않은 행동에는 처벌이라는 피드백을 통해서 행동에 대해 학습

## 3. Clustering
* Unsupervised Learning Algorithm의 한 종류
* 목적
  * 주어진 데이터들이 얼마나, 어떻게 유사한지 보여줌
  * 주어진 데이터셋을 요약/정리하는데 있어서 매우 효율적인 방법들중 하나로 사용
  * 정답을 보장하진 않아서 예측보단 EDA를 위한 방법으로 많이 쓰임
* 종류
  * Hierarchical
    * Agglomerative: 개별 포인트에서 시작후 점점 크게 합쳐감
    * Divisive: 한개의 큰 cluster에서 시작후 점점 작은 cluster로 나눠감
  * Point Assignment
    * 시작시에 cluster의 수를 정한 다음, 데이터들을 하나씩 cluster에 배정시킴
  * Hard vs Soft Clustering
    * Hard Clustering에서 데이터는 하나의 cluster에만 할당됩니다.
    * Soft Clustering에서 데이터는 여러 cluster에 확률을 가지고 할당됩니다.
  * Similarity
    * Euclidean
    * Cosine
    * Jaccard
    * Edit Distance
    * Etc.

* K-Means Clustering  
    * 과정 :
      * n-차원의 데이터에 대해서 :
        * 1) k 개의 랜덤한 데이터를 cluster의 중심점으로 설정
        * 2) 해당 cluster에 근접해 있는 데이터를 cluster로 할당
        * 3) 변경된 cluster에 대해서 중심점을 새로 계산
        * cluster에 유의미한 변화가 없을 때 까지 2-3을 반복
      * 중심점 (Centroid) 계산
        * 주어진 cluster 내부에 있는 모든 점들의 중심부분에 위치한 (가상의) 점
      * 랜덤한 포인트를 가상 cluster의 centroid로 지정
      * 그래프에 표기
    * K-means에서 K를 결정하는 방법
      * The Eyeball Method :사람의 주관적인 판단을 통해서 임의로 지정하는 방법
      * Metrics : 객관적인 지표를 설정하여, 최적화된 k를 선택하는 방법
    * Scikit-learn 사용
```ipython
from sklearn.cluster import KMeans 
kmeans = KMeans(n_clusters = 3)
kmeans.fit(x)
labels = kmeans.labels_
```