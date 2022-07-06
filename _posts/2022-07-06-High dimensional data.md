---
title: 'High dimensional data'
use_math: true
categories:
  - data
---

**목차**  
[1. Vector transformation (벡터변환)](#1-vector-transformation벡터-변환)  
[2. 고유벡터](#2-고유벡터-eigenvector)  
[3. 고유값](#3-고유값-eigenvalue)  
[4. 높은 feature일 경우](#4-높은-feature일-경우)  
[5. PCA](#5-principal-component-analysis-pca)  


---
* Contents
  1. Vector transformation
  2. eigenvector / eigenvalue
  3. PCA 목적, 원리

---

## 1. Vector transformation(벡터 변환)
* 2차원의 공간에서 벡터를 변환하는 것, 즉, 선형 변환은 임의의 두 벡터를 **더하거나** 혹은 스칼라 값을 **곱하는 것**을 의미한다.
  * 임의의 두 벡터 더해서 방향 바꾸기: $T(u+v) = T(u)+T(v)$
  * 스칼라 값을 곱해서 크기 바꾸기: $T(cu)=cT(u)$

## 2. 고유벡터 (Eigenvector)
*  transformation에 영향을 받지 않는 회전축, (혹은 벡터)을 공간의 고유벡터 (Eigenvector)라고 한다.
*  주어진 transformation에 대해서 크기만 변하고 방향은 변화 하지 않는 벡터

## 3. 고유값 (Eigenvalue)
* 변화하는 특정 스칼라 값을 고유값 (eigenvalue)

## 4. 높은 feature일 경우
* overfitting 문제 발생함.
* Feacture Selection:
  * 데이터셋에서 덜 중요한 feature를 제거 하는 방법을 의미
  * 장점 : feature 들간의 연관성 고려됨. feature수 많이 줄일 수 있음
  * 단점 : feature 해석이 어려움.
  * 예시 : PCA, Auto-encoder 등
* Feature Extraction
  * 장점 : 선택된 feature 해석이 쉽다.
  * 단점 : feature들간의 연관성을 고려해야함.
  * 예시 : LASSO, Genetic algorithm 등

## 5. Principal Component Analysis (PCA)
* 고차원 데이터를 효과적으로 분석 하기 위한 기법
* 낮은 차원으로 차원축소
* 고차원 데이터를 효과적으로 시각화 + clustering
* 원래 고차원 데이터의 정보(분산)를 최대한 유지하는 벡터를 찾고, 해당 벡터에 대해 데이터를 (Linear)Projection

* PCA Process
```ipython
  # 1) 데이터를 준비
import numpy as np

X = np.array([ 
              [0.2, 5.6, 3.56], 
              [0.45, 5.89, 2.4],
              [0.33, 6.37, 1.95],
              [0.54, 7.9, 1.32],
              [0.77, 7.87, 0.98]
])
print("Data: ", X)

  # 2) 각 열에 대해서 평균을 빼고, 표준편차로 나누어서 Normalize를 함.
standardized_data = ( X - np.mean(X, axis = 0) ) / np.std(X, ddof = 1, axis = 0)
print("\n Standardized Data: \n", standardized_data)

  # 3) Z의 분산-공분산 매트릭스를 계산함
covariance_matrix = np.cov(standardized_data.T)
print("\n Covariance Matrix: \n", covariance_matrix)

  # 4) 분산-공분산 매트릭스의 고유벡터와 고유값을 계산함
values, vectors = np.linalg.eig(covariance_matrix)
print("\n Eigenvalues: \n", values)
print("\n Eigenvectors: \n", vectors)

  # 5) 데이터를 고유 벡터에 projection 시킴. (matmul)
Z = np.matmul(standardized_data, vectors)

print("\n Projected Data: \n", Z)

  # 6) 시각화
df = pd.DataFrame({"x1": [0.2, 0.45, 0.33, 0.54, 0.77] , "x2": [5.6, 5.89, 6.37, 7.9, 7.87], 'x3': [3.56, 2.4, 1.95, 1.32, 0.98]})

threedee = plt.figure().gca(projection = '3d')
threedee.scatter(df['x1'], df['x2'], df['x3'])
threedee.set_xlabel('x1')
threedee.set_ylabel('x2')
threedee.set_zlabel('x3')
plt.show()

df = pd.DataFrame({"pc1": [-2.1527, -0.6692, -0.4718, 1.2533, 2.0404], "pc2": [-0.0616, 0.4912, -0.2798, -0.4703, 0.3204]})
plt.scatter(df['pc1'], df['pc2'])
plt.title("Data After PCA")
plt.xlabel('pc1')
plt.ylabel('pc2')
plt.show()

  # 라이브러리 이용
from sklearn.preprocessing import StandardScaler, Normalizer
from sklearn.decomposition import PCA

print("Data: \n", X)

scaler = StandardScaler()
Z = scaler.fit_transform(X)
print("\n Standardized Data: \n", Z)

pca = PCA(2)

pca.fit(Z)

print("\n Eigenvectors: \n", pca.components_)
print("\n Eigenvalues: \n",pca.explained_variance_)

B = pca.transform(Z)
print("\n Projected Data: \n", B)
```
* PCA의 특징
  * 데이터에 대해 독립적인 축을 찾는데 사용 할 수 있음.  
  * 데이터의 분포가 정규성을 띄지 않는 경우 적용이 어려움  
    * 이 경우는 커널 PCA 를 사용 가능  
  * 분류 / 예측 문제에 대해서 데이터의 라벨을 고려하지 않기 때문에 효과적 분리가 어려움  
    * 이 경우는 PLS 사용 가능  
