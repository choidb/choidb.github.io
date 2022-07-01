# Hypothesis Test(가설 검정)

**목차**  
[1. 기술 통계치](#1-기술-통계치descriptive-statistics)  
[2. 추리 통계치](#2-추리-통계inferential-statistics)  
[3. ffective Sampling](#3-effective-sampling)  
[4. 가설 검정](#4-가설-검정)  
[5. 표본 평균의 표준 오차](#5-표본-평균의-표준-오차--standard-error-of-the-sample-mean)  
[6. t-test](#6-t-test)  


---
* Contents
  1. Estimation / Sampling의 목적과 방법
  2. 가설검정
  3. T-test의 목적과 사용예시

>
* Keywards
  * 기술 통계치(Descriptive Statistics)의 시각화
    * boxplot
    * bagplot
    * violin plot
  * 추리 통계치(Inferential Statistics)
    * Population
    * Parameter
    * Statistic
    * Estimator
    * Standard Deviation
    * Standard Error
  * Effective Sampling
  * T-test
  * P-value

---

## 1. 기술 통계치(Descriptive Statistics)
* 수집한 데이터를 요약 묘사 설명하는 통계 기법
* count, mean, standard dev, min, 1Q, median, 3Q, max 등의 데이터를 그려서 설명하는 것(혹은 통계치)
* 평균,중앙값,최빈값,표준편차,사분위 등으로 있는 사실에 대해 통계를 내린 것!
* 기술 통계치의 시각화
    * boxplot  
      <img src="../images1/2022-06-13-14-55-17.png" width="400" height="200"/>
    * bagplot  
      <img src="2022-06-13-14-55-53.png" width="400" height="200"/>
    * violin plot  
      <img src="2022-06-13-14-58-13.png" width="400" height="200"/>

* 기술통계는 추리통계를 위한 추진력을 얻기위함

## 2. 추리 통계(Inferential statistics)
* 수집한 데이터를 바탕으로 추론 예측하는 통계 기법
* 기술통계를 바탕으로 알고자 하는 사실을 추론하고 예측

## 3. Effective Sampling
* Simple Random Sampling
  * 모집단에서 sampling을 무작위로 하는 방법
* Systematic Sampling
  * 모집단에서 sampling을 할 때 규칙을 가지고 추출하는 방법
* Stratified Random Sampling
  * 모집단을 미리 여러 그룹으로 나누고, 그 그룹별로 무작위 추출을 수행하는 방법
* Cluster Sampling
  * 모집단을 미리 여러 그룹으로 나누고, 이후 특정 그룹을 무작위로 선택하는 방법

## 4. 가설 검정
* 주어진 상황에 대해서, 하고자 하는 주장이 맞는지 아닌지를 판정하는 과정.
* 모집단의 실제 값에 대한 sample의 통계치를 사용해서 통계적으로 유의한지 아닌지 여부를 판정
* np.random.seed(0)
  * 난수를 예측가능하도록 만듦
  * 시드 재설정 (매번)을 사용할 때마다 동일한 숫자 세트가 나타남
    * 시드를 설정할 때마다 (매번) 동일한 작업을 수행하여 동일한 번호를 부여
    * 결과를 동일하게 만들기 위함이다.

## 5. 표본 평균의 표준 오차 ( Standard Error of the Sample Mean )
* s (우측) = 표본의 표준편차 (sample standard deviation)
* n = 표본의 수 (sample size)
* 결론: 표본의 수가 더욱 많아질수록, 추측은 더 정확해지고 (평균) 높은 신뢰도를 바탕으로 모집단에 대해 예측 할 수 있도록 함

## 6. t-test
* One Sample t-test
  * 1개의 sample 값들의 평균이 특정값과 동일한지 비교.
```ipython
import pandas as pd
from scipy import stats
crab = pd.DataFrame({'0': [25.8, 24.6, 26.1, 22.9, 25.1]})
crab
	0
0	25.8
1	24.6
2	26.1
3	22.9
4	25.1

crab_ttest = stats.ttest_1samp(crab, 23.0)
print("T-value = %.3f, p-value = %.3f" % crab_ttest) # %.3f : 각각 소수점 3자리까지 출력
>>> T-value = 3.364, p-value = 0.028
# 검정통계량 t값은 1.062, p값은 0.348로
# 유의수준 0.05에서(기각역을 p < 0.05로 설정했을 때) 귀무가설을 기각한다.(버린다.)
# 평균값 24.9에 가까울수록 p는 1에 가까워진다.
```
* T-test Process
1) 귀무 가설 (Null Hypothesis) 를 설정 (fair coin, p = 0.5)  
$H_0: \mu = \bar{x}$  
$\mu$: 모집단의 평균  
$\bar{x}$: 표본의 평균  
2) 대안 가설 (Alternative Hypothesis) 를 설정 (not fair coin, p != 0.5)  
$H_1: \mu \neq \bar{x}$
3) 신뢰도를 설정 (Confidence Level) : 모수가 신뢰구간 안에 포함될 확률 (보통 95, 99% 등을 사용)  
신뢰도 95%의 의미  
= 모수가 신뢰 구간 안에 포함될 확률이 95%  
= 귀무가설이 틀렸지만 우연히 성립할 확률이 5%  
<img src="2022-06-13-17-52-28.png" width="400" height="300"/>  

4) P-value를 확인

* P-value 는, 주어진 가설에 대해서 "얼마나 근거가 있는지"에 대한 값을 0과 1사이의 값으로 scale한 지표.
* p-value가 낮다는 것은, 귀무가설이 틀렸을 확률이 높다.
  * 예를 들어서 p-value가 0.05다. -> 우리가 뽑은 샘플 데이터로 낼 수 있는 결론이 귀무 가설이 (틀렸지만 우연히 맞을 확률) 확률이 0.05 다: 귀무가설은 틀렸다

5) 이후 p-value를 바탕으로 가설에 대해 결론을 내림

**[p-value의 기준](https://en.wikipedia.org/wiki/P-value)**

1) p-value < 0.01 : 귀무가설이 옳을 확률이 1%이하 -> 틀렸다 (깐깐한 기준)
2) p-value < 0.05 (5%) : 귀무가설이 옳을 확률이 5%이하 -> 틀렸다 (일반적인 기준)
* 0.05 ~ p-value ~ 0.1 사이인 경우: (애매함)  
실험을 다시한다.  
데이터를 다시 뽑는다.  
샘플링을 다시한다  
기존의 경험 / 인사이트를 바탕으로 가설에 대한 결론을 내린다.  
3) p-value > 0.1 (10%) : 귀무가설이 옳을 확률이 10%이상인데 -> 귀무가설이 맞다 ~ 틀리지 않았을것이다

**One-side test vs Two-side test**

* Two side (tail / direction) test : 샘플 데이터의 평균이 "X"와 같다 / 같지 않다. 를 검정하는 내용

* One side test : 샘플 데이터의 평균이 "X"보다 크다 혹은 작다 / 크지 않다 작지 않다. 를 검정하는 내용

* Two Sample T-test:  
stats.ttest_ind() 사용
