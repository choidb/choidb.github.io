---
title: 'Data Manipulation'
use_math: true
categories:
  - data
---

**목차**  
[1. pandas 로 데이터 합치기](#1-pandas-로-데이터-합치기)  
[2. Tidy 데이터(깔끔한 데이터)](#2-tidy-데이터깔끔한-데이터)  

---
* Contents
  1. pandas 로 데이터 합치기
  2. wide와 tidy 형태의 데이터

>
* Keywards
  * concat / merge
  * tidy 데이터
  * melt와 pivot / pivot_table 함수
    * wide와 tidy 형태의 데이터를 서로 변환

---
[Top_25_pandas_tricks 영상 스크립트 및 코드](https://nbviewer.org/github/justmarkham/pandas-videos/blob/master/top_25_pandas_tricks.ipynb)

## 1. pandas 로 데이터 합치기
* Concat (Concatenate)
  
```python
>>> df1 = pd.DataFrame([['a', 1], ['b', 2]],
...                   columns=['letter', 'number'])
>>> df1
  letter  number
0      a       1
1      b       2
>>> df2 = pd.DataFrame([['c', 3], ['d', 4]],
                   columns=['letter', 'number'])
>>> df2
  letter  number
0      c       3
1      d       4
>>> pd.concat([df1, df2])
  letter  number
0      a       1
1      b       2
0      c       3
1      d       4
>>> df3 = pd.DataFrame([['c', 3, 'cat'], ['d', 4, 'dog']],
...                    columns=['letter', 'number', 'animal'])
>>> df3
  letter  number animal
0      c       3    cat
1      d       4    dog
>>> pd.concat([df1, df3], sort=False)
  letter  number animal
0      a       1    NaN
1      b       2    NaN
0      c       3    cat
1      d       4    dog

출처: https://pandas.pydata.org/docs/reference/api/pandas.concat.html
```
* Merge
  * concat과 다르게 공통된 부분을 기반으로 합치기

```python
>>> df1 = pd.DataFrame({'lkey': ['foo', 'bar', 'baz', 'foo'],
...                     'value': [1, 2, 3, 5]})
>>> df2 = pd.DataFrame({'rkey': ['foo', 'bar', 'baz', 'foo'],
                    'value': [5, 6, 7, 8]})
>>> df1
    lkey value
0   foo      1
1   bar      2
2   baz      3
3   foo      5
>>> df2
    rkey value
0   foo      5
1   bar      6
2   baz      7
3   foo      8

>>> df1.merge(df2, left_on='lkey', right_on='rkey')
  lkey  value_x rkey  value_y
0  foo        1  foo        5
1  foo        1  foo        8
2  foo        5  foo        5
3  foo        5  foo        8
4  bar        2  bar        6
5  baz        3  baz        7

출처: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html
```

* Conditioning
  * 데이터 프레임의 부분 선택
  * 데이터프레임 필터링 예시  
    * & 와 | 활용
    * type cast
```python
df['순이익률'] = pd.to_numeric(df['순이익률'])

condition = ( (df['순이익률'] > 0) & (df['순이익률'] < 10))
df_subset2 = df[condition]
```

* isin
  * Dataframe의 컬럼에서 어떤 list의 값을 포함하고 있는것만 걸러낼 때 사용  

```python
df = pd.DataFrame({'num_legs': [2, 4], 'num_wings': [2, 0]},
                  index=['falcon', 'dog'])
df
        num_legs  num_wings
falcon         2          2
dog            4          0

>>> df.isin([0, 2])
        num_legs  num_wings
falcon      True       True
dog        False       True

출처: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.isin.html
```

* Groupby
  * 같은 값을 하나로 묶어 통계 또는 집계 결과를 얻기 위해 사용하는 것

```python
>>> df = pd.DataFrame({'Animal': ['Falcon', 'Falcon',
                              'Parrot', 'Parrot'],
                   'Max Speed': [380., 370., 24., 26.]})
>>> df
   Animal  Max Speed
0  Falcon      380.0
1  Falcon      370.0
2  Parrot       24.0
3  Parrot       26.0

>>> df.groupby(['Animal']).mean()
        Max Speed
Animal
Falcon      375.0
Parrot       25.0

출처: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html
```

## 2. Tidy 데이터(깔끔한 데이터)
* Tidy 데이터
  * 행과 열이 전치 (transpose) 되어 있어 보이는 레이아웃
1. 각 변수는 열을 구성
2. 각 관측치는 행을 구성
3. 각 관측단위는 표를 구성

* 지저분한 데이터
1. 열 이름(Column header)이 변수 이름이 아니고 값인 경우
2. 같은 표에 다양한 관측 단위(observational units)가 있는 경우
3. 하나의 열(column)에 여러 값이 들어 있는 경우변수가 행과 열에 모두 포함되어 있는 경우
4. 변수가 행과 열에 모두 포함되어 있는 경우
5. 하나의 관측 단위(observational units)가 여러 파일로 나누어져 있는 경우

* Tidy 데이터로 만드는 방법
  * pandas 의 melt 함수를 사용
* Tidy --> Wide 로 바꾸는 방법
  * .pivot_table() 사용

