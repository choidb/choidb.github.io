---
title: 'Evaluation Metrics for Classification'
use_math: true
categories:
  - ml
---

**목차**  
[1. Confusion matrix](#1-confusion-matrix)  
[2. 정밀도(precision), 재현율(recall)](#2-정밀도precision-재현율recall)  
[3. ROC, AUC (Receiver Operating Characteristic, Area Under the Curve)](#3-roc-auc-receiver-operating-characteristic-area-under-the-curve)  


---
* Contents
1. Confusion matrix
2. 정밀도, 재현율
3. ROC curve, AUC 점수

---

## 1. Confusion matrix
* 분류 모델의 성능 평가 지표를 보여줌
* sklearn.metrics.plot_confusion_matrix를 사용
![](2022-06-24-11-21-13.png)
<img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images2/2022-06-24-11-21-13.png?raw=true" width="1000" height="1000"/>


## 2. 정밀도(precision), 재현율(recall)
* [Scikit-Learn User Guide — Classification Report](https://scikit-learn.org/stable/modules/model_evaluation.html#classification-report)
- 정확도(Accuracy)는 전체 범주를 모두 바르게 맞춘 경우를 전체 수로 나눈 값입니다: $\large \frac{TP + TN}{Total}$

- 정밀도(Precision)는 **Positive로 예측**한 경우 중 올바르게 Positive를 맞춘 비율입니다: $\large \frac{TP}{TP + FP}$

- 재현율(Recall, Sensitivity)은 **실제 Positive**인 것 중 올바르게 Positive를 맞춘 것의 비율 입니다: $\large \frac{TP}{TP + FN}$

- F1점수(F1 score)는 정밀도와 재현율의 조화평균(harmonic mean)입니다:  $ 2\cdot\large\frac{precision\cdot recall}{precision + recall}$

* 다루는 문제에 따라 정밀도와 재현율 중 어느 평가지표를 우선시 해야하는지 판단해야함
* 임계값을 낮추면 백신을 접종할 확률이 굉장히 낮은 사람들에 대해서만 0으로 분류하게 됩니다.
* 임계값을 낮추면 백신을 접종하지 않은 사람들에 대한 정밀도는 올라가지만 재현율은 떨어질 것임
* 모든 임계값을 한 눈에 보고 모델을 평가할 수 있는 방법??
  * &rArr; ROC curve 사용

## 3. ROC, AUC (Receiver Operating Characteristic, Area Under the Curve)
* 분류문제에서 여러 임계값 설정에 대한 모델의 성능을 구할 수 있게됨
* ROC curve는 여러 임계값에 대해 TPR(True Positive Rate, recall)과 FPR(False Positive Rate) 그래프를 보여줌
* [Receiver operating characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) 참고
* **Recall(재현율) = Sensitivity** = ${\displaystyle \mathrm {TPR} ={\frac {\mathrm {TP} }{\mathrm {P} }}={\frac {\mathrm {TP} }{\mathrm {TP} +\mathrm {FN} }}=1-\mathrm {FNR} }$

* **Fall-out(위양성률)** = ${\displaystyle \mathrm {FPR} ={\frac {\mathrm {FP} }{\mathrm {N} }}={\frac {\mathrm {FP} }{\mathrm {FP} +\mathrm {TN} }}=1-\mathrm {TNR(Specificity)} }$
* 재현율을 높이기 위해서는 Positive로 판단하는 임계값을 계속 낮추어 모두 Positive로 판단하게 만들면 됩니다. 하지만 이렇게 하면 동시에 Negative이지만 Positive로 판단하는 위양성률도 같이 높아집니다.
* 재현율은 최대화 하고 위양성률은 최소화 하는 임계값이 최적의 임계값이다.
* AUC 는 ROC curve의 아래 면적임
* [Understanding ROC curves](http://www.navan.name/roc/)
* 사이킷런 roc_curve는 임계값에 따른 TPR, FPR 수치를 자동으로 계산해줌
* ROC curve는 이진분류문제에서 사용할 수 있습니다. 
* 다중분류문제에서는 각 클래스를 이진클래스 분류문제로 변환(One Vs All)하여 구할 수 있습니다.
  * 3-class(A, B, C) 문제 -> A vs (B,C), B vs (A,C), C vs (A,B) 로 나누어 수행
