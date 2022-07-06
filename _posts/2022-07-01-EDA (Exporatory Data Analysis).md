---
title: "EDA(Exporatory Data Analysis)"
use_math: true
categories:
  - data
---


**목차**  
[1. 데이터셋 불러오기](#1-데이터셋-불러오기)  
[2. EDA(edaexploratory-data-analysis)](#2-edaexploratory-data-analysis)  
[3. 데이터 전처리(data-preprocessing)](#3-데이터-전처리-data-preprocessing)  


---
* Contents
  1. 데이터 불러오기
  2. 데이터 분석
  3. 데이터 모델링
>
* Keywards
  * EDA
  * pre-processing

---
## 1. 데이터셋 불러오기

* 데이터셋을 불러오기 위한 단계:
  1. Description을 통해 데이터셋에 대한 정보를 파악합니다.
  * 행과 열의 수
  * 열에 헤더가 있는지 ("데이터 이름"이 있는지?)
  * 결측 데이터 (Missing data)가 있는지 확인
  * 원본의 형태를 확인하기

  2. pandas.read_csv()를 사용하여 데이터셋 불러오기
  * 데이터셋을 확인하는 방법

```IPython
# 1-1. URL을 통해서 불러오기
import pandas as pd
url = '데이터셋 주소'
df = pd.read_csv(url) 
# pd라이브러리의 read_csv를 사용하여 url에 있는 데이터를 읽고, df라는 변수에 저장
df.head()
```
```Ipython
# 1-2. 로컬 파일로 부터 데이터셋 불러오기 (CSV)
  # 방법 1. 구글 코랩 파일 업로드 패키지
from google.colab import files
uploaded = files.upload()

  # 방법 2: GUI (Graphical User Interface) 사용
df = pd.read.csv('adult (6).data') # after upload
print(df.shape)
```

## 2. EDA(Exploratory Data Analysis)

* EDA
  * EDA란, 데이터 분석에 있어서 매우 중요한, 초기 분석의 단계를 의미하며
  * 시각화 같은 도구를 통해서 패턴을 발견하거나
  * 데이터의 특이성을 확인하거나
  * 통계와 그래픽 (혹은 시각적 표현)을 통해서 가설을 검정하는 과정 등을 포함
* EDA의 방법 2가지 (Graphic, Non-Graphic)
  * Graphic : 차트 혹은 그림 등을 이용하여 데이터를 확인하는 방법입니다.
  * Non-Graphic :그래픽적인 요소를 사용하지 않는 방법으로, 주로 Summary Statistics를 통해 데이터를 확인하는 방법입니다.
* EDA의 "타겟"(데이터) 또한 2가지 (Univariate, Multi-variate)로 나눠짐
  * Multi-variate 의 경우 여러 변수들간의 관계를 보는 것이 주요 목적이다.

* Uni - Non Graphic
  * Sample Data의 Distribution을 확인하는 것이 주목적
  * Numeric data의 경우 summary statistics를 주로 활용
    * Center (Mean, Median, Mode)
    * Spread (Variance, SD, IQR, Range)
    * Modality (Peak)
    * Shape (Tail, Skewness, Kurtosis)
    * Outliers 등을 확인
  * Categorical data의 경우 occurence, frequency, tabulation 할 수 있음.
* Uni - Graphic
  * Histogram 혹은 Pie chart, Stem-leaf plot, Boxplot, QQplot 등을 사용합니다.
  * 만약 값들이 다양하다면, Binning, Tabulation등을 활용함.
* QQPlot
  * 데이터의 분포와 이론상 분포가 잘 일치하는가 를 확인 할 수 있는 방법
* Multi - Non Graphic
  * Relationship을 보는 것이 주된 목표이며
  * 사용  
    * Cross-Tabulation
    * Cross-Statistics (Correlation, Covariance)
* Categorical 데이터
  * Cross-Tabulation을 적용할 수 있음
  * Numerical Feature들의 경우 Cross Statistics를 통해 EDA
* Multi - Graphic
  * Category & Numeric : Boxplots, Stacked bar, Parallel Coordinate, Heatmap
* pandas를 사용한 기초 EDA  
**Useful Pandas Functions**
  * Missing Data
    * isna
    * isnull
    * notna
    * notnull
    * dropna
    * fillna
>
  * Data Frame
    * index
    * columns
    * dtypes
    * info
    * select_dtypes
    * loc
    * iloc
    * insert
    * head
    * tail
    * apply
    * aggregate
    * drop
    * rename
    * replace
    * nsmallest
    * nlargest
    * sort_values
    * sort_index
    * value_counts
    * describe
    * shape
  * Vis
    * plot
    * plot.area
    * plot.bar
    * plot.barh
    * plot.box
    * plot.density
    * plot.hexbin
    * plot.hist
    * plot.kde
    * plot.line
    * plot.pie
    * plot.scatter

## 3. 데이터 전처리 (Data Preprocessing)
* Cleaning
  * noise 를 제거하거나, inconsistency 를 보정하는 과정
* Missing Values
  * Ignore the tuple (결측치가 있는 데이터 삭제)
  * Manual Fill (수동으로 입력)
  * Global Constant ("Unknown")
  * Imputation (All mean, Class mean, Inference mean, Regression 등)
* Noisy data
  * Noise란, 큰 방향성에서 벗어난 random error 혹은 variance를 포함하는 데이터
  * descriptive statistics 혹은 visualization등 (eda)을 통해 제거가 가능
* Integration
  * 여러개로 나누어져 있는 데이터들을 분석하기 편하게 하나로 합치는 과정
* Transformation
  * 데이터의 형태를 변환하는 작업으로, scaling이라고 부르기도 함.
* Reduction
  * 데이터를 의미있게 줄이는 것을 의미



