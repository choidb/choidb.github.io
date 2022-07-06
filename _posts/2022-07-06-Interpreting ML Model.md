---
title: 'Interpreting ML Model'
use_math: true
categories:
  - ml
---

**목차**  
[1. Partial Dependence Plots(PDP)](#1-partial-dependence-plotspdp)  
[2. SHAP 라이브러리를 이용](#2-shap-라이브러리를-이용)

---
* Contents
1. 부분의존도그림(Partial dependence plot, PDP)
2. 개별 예측 사례를 Shap value plots을 사용해 설명

---

## 1. Partial Dependence Plots(PDP)
* 복잡한 모델 -> 이해하기 어렵지만 성능이 좋다.
* 단순한 모델 -> 이해하기 쉽지만 성능이 부족하다.
* 특성의 값에 따라서 타겟값이 증가/감소하느냐와 같은 어떻게 영향을 미치는지에 대한 정보
  * &rArr; 부분의존도그림(Partial dependence plots, PDP)을 사용
    * 관심있는 특성들이 타겟에 어떻게 영향을 주는지 쉽게 파악

<img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images2/2022-06-24-13-06-25.png?raw=true" width="800" height="600"/>

* PDP에서 카테고리특성을 사용
  * 카테고리 특성을 학습할 때 Ordinal Encoder, Target Encoder 같은 인코더를 사용하게 되는데, 인코딩을 하게되면 학습 후 PDP 를 그릴 때 인코딩된 값이 나오게 되어 카테고리특성의 실제 값을 확인하기 어려운 문제가 있음.

## 2. SHAP 라이브러리를 이용
* [SHAP(SHapley Additive exPlanations)](https://github.com/slundberg/shap)
* [Shapley Values](https://datanetworkanalysis.github.io/2019/12/23/shap1)
* Shapley values
  * 특성 갯수가 많아질 수록 Shapley value를 구할 때 필요한 계산량이 기하급수적으로 늘어남
  * SHAP에서는 샘플링을 이용해 근사적으로 값을 구하며 SHAP을 통해 구하는 값은 Shap value라고 부른다.

참고자료  
PDPbox
- [PDPbox library documentation](https://pdpbox.readthedocs.io/en/latest/)
- [PDP Gallery](https://github.com/SauceCat/PDPbox#gallery)
- [pdpbox.pdp.pdp_isolate](https://pdpbox.readthedocs.io/en/latest/pdp_isolate.html#pdpbox-pdp-pdp-isolate)
- [pdpbox.pdp.pdp_plot](https://pdpbox.readthedocs.io/en/latest/pdp_plot.html#pdpbox-pdp-pdp-plot)
- [pdpbox.pdp.pdp_interact](https://pdpbox.readthedocs.io/en/latest/pdp_interact.html#pdpbox-pdp-pdp-interact)
- [pdpbox.pdp.pdp_interact_plot
](https://pdpbox.readthedocs.io/en/latest/pdp_interact_plot.html#pdpbox-pdp-pdp-interact-plot)

SHAP
- [SHAP](https://github.com/slundberg/shap)
- [Welcome to the SHAP Documentation](https://shap.readthedocs.io/en/latest/index.html)
- [One Feature Attribution Method to (Supposedly) Rule Them All: Shapley Values](https://towardsdatascience.com/one-feature-attribution-method-to-supposedly-rule-them-all-shapley-values-f3e04534983d)
- [Explain Your Model with the SHAP Values](https://towardsdatascience.com/explain-your-model-with-the-shap-values-bc36aac4de3d)
