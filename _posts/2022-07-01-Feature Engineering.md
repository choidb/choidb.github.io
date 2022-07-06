---
title: 'Feature Engineering'
use_math: true
categories:
  - data
---

**목차**  
[1. Feature Engineering](#1-feature-engineering)  
[2. String](#2-string)  
[3. Apply](#3-apply)  
[4. python의 6가지 데이터 타입](#4-python의-6가지-데이터-타입)

---
* Contents
  1. Feature Engineering
  2. Understand Python Data Types in 10 minutes

>
* Keywards
  * Feature Engineering 
  * pandas의 문자열(string)
  * .apply()

---

## 1. Feature Engineering
* Feature Engineering은 도메인 지식과 창의성을 바탕으로, 데이터셋에 존재하는 Feature들을 재조합하여 새로운 Feature를 만드는 것
* DataFrame: 테이블 형태의 데이터
* Dataset: 특정한 작업을 위해서 데이터를 관련성 있게 모아놓은 것
```ipython
df.dtypes # data type 확인. object, float64, int64 등
```
* Na(NaN), Null, 0, Undefined, None 차이
  * Na(NaN), Null: 아직 정해지지 않는 값. 
    * NaN: not a number. 숫자가 아닌 다른 원시형으로 해석하여 출력된 값
    * Null: 선언, 등록을 하는 키워드. 값은 값이지만 값으로써 의미없는 특정한 값이 등록되어 있는 것
  * None: 비어있는 값
  * Undefined: (미리 선언된 전역변수(전역 객체의 프로퍼티))선언은 되었으나 값이 할당 되지 않은 상태. 변수의 값이 등록 되어있지 않기 때문에 초기값으로 자동 정의된 것이다.

## 2. String
* 방법
  * 문자를 숫자로 바꾸기 위해 숫자가 아닌 부분을 제거
  * 문자를 숫자로 형변환한다.
* string replace
```ipython
testString = '25,970'
testString.replace(',','')
>> '25970'
```
* Type casting
  * 변수의 type을 강제로 다른 type으로 변경하는 것

## 3. Apply
```ipython
# 컬럼 단위로 문자열에 적용하는 방법
df['열이름'] = df['열이름'].apply(toInt)
df
```

## 4. python의 6가지 데이터 타입
Numeric Types: int(정수), float(소수), complex(복소수)  
Sequence Types: str(문자열), list(리스트), tuple(튜플)  
Mapping Type: dict(딕셔너리)  
Set Types: set(집합)  
Boolean Type: bool(불리언)  
Binary Types: bytes, bytearray, memoryview
