---
title: 'Data Wrangling'
use_math: true
categories:
  - ml
---

**목차**  
[1. 데이터 랭글링](#1-데이터-랭글링)  

---
* Contents
1. 지도학습을 위한 데이터 엔지니어링 방법을 이해하고 올바른 특성 만들기

---

## 1. 데이터 랭글링
* 데이터 랭글링(wrangling)은 분석을 하거나 모델을 만들기 전에 데이터를 사용하기 쉽게 변형하거나 맵핑하는 과정
* 보통 모델링 과정 중 가장 많은 시간이 소요되는 단계

* 데이터 랭글링은 총 5단계로 구분됩니다.

1. Gather
 - 데이터를 얻는 방법으로는 다운로드(Download), 웹 스크레이핑(Web scrapping), API(Application Programming Interface)가 있습니다.

2. Assess
 - 얻은 데이터를 읽고 데이터가 깨끗한지 아닌지 판단하는 단계입니다.

3. Clean
 - 데이터를 정제하는 방법으로는 Define, Code, Test가 있습니다. 2단계(Assess)에서 발견된 데이터의 문제점을 보고 어떤 부분을 정제할지 정의하고(Define), 정제하기 위한 코드를 짜고(Code), 잘 정제가 되었는지 테스트를 해보는(Test) 것입니다.

4. Reassess and Iterate
 - 다시 2단계로 돌아가 데이터가 잘 정제되었는지 판단을 합니다. 추가로 정제해야 할 부분이 있다면 다시 2-3-4 단계를 반복합니다.

5. Store (optional)
 - 나중에 다시 사용하기 위해 저장하는 단계입니다.

이번 챕터에서는 1단계인 Gathering Data에 대해 알아보겠습니다.

Gathering 단계에는 다운로드, 웹 스크레이핑, API를 활용하는 방법이 있다고 했습니다.

출처: [Data Wrangling (Gathering Data)](https://bkshin.tistory.com/entry/DATA-23-Data-Wrangling)
