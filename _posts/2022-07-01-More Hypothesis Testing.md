# More Hypothesis Testing

**목차**  
[1. t-test-전제-조건](#1--t-test-전제-조건)  
[2. type-of-error](#2-type-of-error)  
[3. more-hypothesis-testing](#3-more-hypothesis-testing)  
[4. chi2-tests](#4-chi2-tests)  
[5. two-sample-chi2-test](#5-two-sample-chi2-test)  
[6. chi2_contingency-결과-해석](#6-chi2_contingency-결과-해석)  


---
* Contents
  1. t-test를 위한 조건
  2. t-test외에 다른 가설검정 방법
  3. Type of Error
  4. $\chi^2$-test의 목적과 사용예시
  5. 모수통계와 비모수통계의 차이

>
* Keywards
  * 독립성
  * 등분산성
  * 정규성
  * 타입 에러
  * 비모수적 평균 비교법
  * 카이제곱 검정
  * 자유도

---

## 1.  t-test 전제 조건

* 독립성 : 두 그룹이 연결되어 있는 (paired) 쌍인지
* 등분산성 : 두 그룹이 어느정도 유사한 수준의 분산 값을 가지는지
* 정규성: 데이터가 정규성을 나타는지
  * Normal test(scipy.stats.normaltest)로 normality를 test

## 2. Type of Error

|Table of error types||Null hypothesis (H <sub>0 </sub>) is||
|---:|:---|:---:|:---:|
|||True|False|
|Decision about <br/> Null hypothesis (H <sub>0 </sub>)|Don't reject|Correct inference <br/> (true negative) <br/> (probability = 1−α)|Type II error <br/> (false negative) <br/> (probability = β) |
||Reject|Type I error <br/> (false positive) <br/>(probability = α) |Correct inference <br/> (true positive) <br/> (probability = 1−β)|

* Type I error: 
  * 귀무가설이 실제로 참이지만, 귀무가설을 기각하는 오류
  * 실제 음성인 것을 양성으로 판정
  * 거짓 양성(false positive) 또는 알파 오류라 불림
  * Type I error의 0.05 및 5% 유의수준은 귀무가설이 5% 확률로 잘못 기각된다는 의미
* Type II error:
  * 귀무가설이 실제로 거짓이지만, 귀무가설을 채택하는 오류
  * 실제 양성인 것을 음성으로 판정
  * 거짓 음성 또는 베타 오류라 불림


## 3. More hypothesis testing
* Non-Parametric Methods
  * 모집단이 특정 확률 분포 (normal과 같은)를 따른다는 전제를 하지 않는 방식
  * Categorical 데이터를 위한 모델링 혹은 극단적 outlier가 있는 경우 매우매우 유효한 방식
  * distribution free method라고 부르기도 함.
    * Chisquare
    * Spearman correlation
    * Run test
    * Kolmogorov Smirnov
    * Mann-Whitney U
    * Wilcoxon
    * Kruskal-Wallis(비모수적 평균 비교법) 등
* Kruskal-Wallis Test (비모수적 평균 비교법)
```ipython
# Kruskal-Wallis H-test - 2개 이상 그룹의 중위 랭크를 통한 차이 비교 ( extended X2 )
# 샘플 수가 > 5 일때 좋음 
from scipy.stats import kruskal

x1 = [1, 3, 4, 8, 9]
y1 = [1, 4, 6, 7, 7]
kruskal(x1, y1) # 약간은 다르지만, "유의한" 차이는 아님
>>> KruskalResult(statistic=0.01111111111111548, pvalue=0.91605107228188)

x2 = [12, 15, 18]
y2 = [24, 25, 26]
z = [40, 40]  # 3번째 그룹은 사이즈가 다름
kruskal(x2, y2, z)
>>> KruskalResult(statistic=6.325301204819277, pvalue=0.042313436212501186)
```

## 4. $\chi^2$ Tests
* One sample $\chi^2$ test
  * 주어진 데이터가 특정 예상되는 분포와 동일한 분포를 나타내는지 에 대한 가설검정.
  * Goodness of Fit test라 부르기도 함
* $\chi^2$ 통계치 의 계산식  

$\chi^2 = \sum \frac{(observed_i-expected_i)^2}{(expected_i)}$  

각 차이의 값을 제곱하는 것으로, 모든 값을 양수로 만들고 관측과 예측값의 차이를 더 강조함

### **Statistics -> P-value로 바꾸기**
* stats.chi2.pdf(x2, df) 사용

```ipython
from scipy import stats

x2 = 0.00139

1 - stats.chi2.cdf(x2, df = ((2-1)*(2-1)) ) # pvalue : 0.97, 연관이 있다.
>>> 0.9702595963009745

import numpy as np
from scipy.stats import chisquare  

s_obs = np.array([[18, 22, 20, 15, 23, 22]]) # Similar
chisquare(s_obs, axis=None) # One sample chi-square
>>> Power_divergenceResult(statistic=2.3000000000000003, pvalue=0.8062668698851285)

ns_obs = np.array([[5, 23, 26, 19, 24, 23]])

chisquare(ns_obs, axis=None)
>>> Power_divergenceResult(statistic=14.8, pvalue=0.011251979028327346)
```

## 5. Two sample $\chi^2$ test
* two sample Chi-squared test는 두 표본집단의 분포가 동일한지 확인할 때 사용
* 표본집단이 연관이 있는지, 없는지를 확인
* continuous data라면, categorical data로 바꿔서 사용해야함.
* crosstab으로 만들어 준다.

```ipython
# 필요한 패키지 import
import pandas as pd
import numpy as np
import seaborn as sns
from scipy import stats

# 데이터셋 불러오기
df = sns.load_dataset("penguins")
df = df.dropna()

# 데이터 프레임 column명 수정
df = df.rename(columns={"species":"species", "island":"island", "bill_length_mm":"bill_length", "bill_depth_mm":"bill_depth",
                        "flipper_length_mm":"flipper_length", "body_mass_g":"body_mass", "sex":"sex"})

mass_cut = pd.cut(df["body_mass"], 3).astype("category")
flipper_cut = pd.cut(df["flipper_length"], 3).astype("category")
data = pd.crosstab(mass_cut, flipper_cut)
data.columns = ["Short", "Middle", "Long"]
data.index = ["Light", "Middle", "Heavy"]

# 귀무가설: 펭귄의 몸무게와 플리퍼 길이는 연관이 없다.
# 대립가설: 펭귄의 몸무게와 플리퍼 길이는 연관이 있다.
# 신뢰도: 95%

chi, pvalue, _, _ = stats.chi2_contingency(data, correction=False)
chi, pvalue
>>> (244.23390701043138, 1.1365768507791132e-51)
# p-value가 0.05보다 작기 때문에 귀무가설을 기각하고 대립가설을 채택
```

**자유도(Degrees of Freedom)**
* 해당 parameter를 결정짓기 위한 독립적으로 정해질 수 있는 값의 수.

## 6. chi2_contingency 결과 해석
1 : $\chi^2$ statistic  
2 : p-value  
3 : degree of freedom  
4 : expected value for Observed  