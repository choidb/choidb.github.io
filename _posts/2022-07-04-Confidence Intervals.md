---
title: 'Confidence Intervals'
use_math: true
---


# Confidence Intervals

**목차**  
[1. ANOVA(ANalysis Of VAriance) 분산 분석](#1-anovaanalysis-of-variance-분산-분석)  
 


---
* Contents
  1. ANOVA
  2. CLT
  3. 신뢰구간의 목적과 사용예시
  4. 신뢰구간 계산


>
* Keywards
  * ANOVA
  * 신뢰구간

---

## 1. ANOVA(ANalysis Of VAriance) 분산 분석
* 분산분석은 3개 이상 다수의 집단을 비교할 때 사용하는 가설검정 방법
* Multiple Comparision
  * 3개를 비교할때 각각 2개씩 3번 비교하게되면 에러가 날 확률이 커지게되므로 한번에 비교할 필요가 있다.
* Variation
  * 여러 그룹들이 하나의 분포에서부터 왔다는 가정으로 지표는 F-statistic 사용
  * $F = { {Variance-between-group} \over {Variance-with-in-group}}$
* 공식  
  * $m$ = 전체 그룹 수, $n$ = 데이터 수

  * $S_{w} = \sum_{i = 1}^{m} \sum_{j=1}^{n} (x_{ij} - x_{i.})^2$
  * $x_{i.} = \sum_{j = 1}^{n} {x_{ij} / n}$
  * $S_{b} = n \sum_{i=1}^m (x_{i.} - x_{..})^2 $
  * $x_{..} = {\sum_{i=1}^m x_{i.} \over {m}}$
  * $F = {{ S_{b}}/{(m-1)} \over S_{w} / (nm-m)}$
  * $p(F_{m-1, nm-m} > F_{m-1, nm-m, \alpha}) = \alpha $

* F-stat by scipy
```python
from scipy.stats import f_oneway
f_oneway(g1, g2, g3) # pvalue = 0.11 
```

* 큰 수의 법칙 ( Law of large numbers )
  * sample 데이터의 수가 커질 수록, sample의 통계치는 점점 모집단의 모수와 같아진다.

* method chaining
  * 메서드가 객체를 반환하게 되면, 메서드의 반환 값인 객체를 통해 또 다른 함수를 호출할 수 있습니다.

* 중심극한정리 ( Central Limit Theorem, CLT )
  * Sample 데이터의 수가 많아질 수록, sample의 평균은 정규분포에 근사한 형태로 나타난다.
  * 샘플링을 몇번하느냐, 얼마나 하느냐에 따라 다름.
* 신뢰도
  * 신뢰도가 95% 라는 의미는 표본을 100번 뽑았을때 95번은 신뢰구간 내에 모집단의 평균이 포함된다.
  * $\bar {x} \pm {t \cdot {s \over \sqrt{n} } }$
  * $\bar{x}$ 를 `estimated mean`.
  * ${t \cdot {s \over \sqrt{n}}}$ 를 `error`라 부릅니다.
