---
title: '자연어처리(NLP, Natural Language Processing)'
use_math: true
categories:
  - dl
---

**목차**  
[1. 자연어처리(NLP, Natural Language Processing)](#1-자연어처리nlp-natural-language-processing)  
[2. 텍스트 전처리(Text Preprocessing)](#2-텍스트-전처리text-preprocessing)  
[3. 등장 횟수 기반의 단어 표현 (Count-based Representation)](#3-등장-횟수-기반의-단어-표현-count-based-representation)  


---
* Contents
1. 자연어처리
2. 불용어(Stop words), 어간추출(Stemming), 표제어추출(Lemmatization)
3. Bag-of-words
4. N-gram


---

## 1. 자연어처리(NLP, Natural Language Processing)
* 자연어(Natural Language)
  * 사람들이 일상적으로 쓰는 언어를 인공적으로 만들어진 언어인 인공어와 구분하여 부르는 개념
* 자연어를 컴퓨터로 처리하는 기술을 자연어 처리(Natural Language Processing, NLP)라고 한다.
* 자연어처리로 할 수 있는 일들
  * 자연어 이해(NLU, Natural Language Understanding)
    * 분류(Classification) : 뉴스 기사 분류, 감성 분석(Positive/Negative)
      * Ex) "This movie is awesome!" -> Positive or Negative?
    * 자연어 추론(NLI, Natural Langauge Inference)
      * Ex) 전제 : "A는 B에게 암살당했다", 가설 : "A는 죽었다" -> True or False?
    * 기계 독해(MRC, Machine Reading Comprehension), 질의 응답(QA, Question&Answering)
      * Ex) 지문을 읽고 질문에 맞는 답변하기
    * 품사 태깅(POS tagging), 개체명 인식(Named Entity Recognition) 등
      * Ex) POS(품사) Tagging :나는() 9시() 까지() 학교() 에() 가야한다()
      * Ex) NER : 나는() 9시() 까지() 학교() 에() 가야한다()
    * 추출 요약(Extractive summerization) : 문서 내에서 해당 문서를 가장 잘 요약하는 부분을 찾아내기
  * 자연어 생성(NLG, Natural Language Generation)
    * 텍스트 생성 (특정 도메인의 텍스트 생성)
      * Ex) 뉴스 기사 생성하기, 가사 생성하기
  * NLU & NLG
    * 기계 번역(Machine Translation)
    * 생성 요약(Absractive summerization) : 해당 문서를 요약하는 요약문을 생성
    * 챗봇(Chatbot)
      * 특정 태스크를 처리하기 위한 챗봇(Task Oriented Dialog, TOD)
        * Ex) 식당 예약을 위한 챗봇, 상담 응대를 위한 챗봇
      * 정해지지 않은 주제를 다루는 일반대화 챗봇(Open Domain Dialog, ODD)
* 자연어 처리가 사용된 서비스 사례
  * 챗봇 : 심리상담 챗봇(트로스트, 아토머스), 일반대화 챗봇(스캐터랩 - 이루다, 마인드로직)
  * 번역 : 파파고, 구글 번역기
* 벡터화(Vectorize)
  * 컴퓨터가 이해할 수 있도록 벡터로 만들어야 한다.
  * 자연어를 어떻게 벡터로 표현하는 지는 자연어 처리 모델의 성능을 결정하는 중요한 역할을 한다.
  * 등장 횟수 기반의 단어 표현(Count-based Representation) : 단어가 문서(혹은 문장)에 등장하는 횟수를 기반으로 벡터화하는 방법
    * Bag-of-Words (CounterVectorizer)
    * TF-IDF (TfidfVectorizer)
  * 분포 기반의 단어 표현(Distributed Representation) : 타겟 단어 주변에 있는 단어를 기반으로 벡터화하는 방법
    * Word2Vec(CBoW, Skip-gram)
    * fastText

## 2. 텍스트 전처리(Text Preprocessing)
* 실제 텍스트 데이터를 다룰 때에는 데이터를 읽어보면서 어떤 특이사항이 있는지 파악해야함
* 전처리 방법
  * 내장 메서드를 사용한 전처리 (lower, replace, ...)
  * 정규 표현식(Regular expression, Regex)
  * 불용어(Stop words) 처리
  * 통계적 트리밍(Trimming)
  * 어간 추출(Stemming) 혹은 표제어 추출(Lemmatization)
1. 차원의 저주 (Curse of Dimensionality)
   * “특성의 개수가 선형적으로 늘어날 때 동일한 설명력을 가지기 위해 필요한 인스턴스의 수는 지수적으로 증가한다. 즉 동일한 개수의 인스턴스를 가지는 데이터셋의 차원이 늘어날수록 설명력이 떨어지게 된다.”
   * 횟수 기반의 벡터 표현에서는 전체 말뭉치에 존재하는 단어의 종류가 데이터셋의 Feature, 즉 차원이 된다.
   * 단어의 종류를 줄여주어야 차원의 저주를 어느정도 해결할 수 있다
   * 각 문장을 문서-단어 행렬로 만든다.
     * 문서-단어 행렬(Document-Term Matrix, DTM)
   * 
2. 대소문자 통일
* 모든 문자를 소문자로 통일하여 같은 범주로 취급해야 한다.
  * EX) Amazonbasics 와 AmazonBasics
3. 정규표현식(Regex)
* replace 와 같은 자체 내장 메서드 사용
* 정규표현식(Regular Expression, Regex) 사용
* [정규 표현식](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)
* [정규 표현식 실습하기](https://regexr.com/)

4. SpaCy를 사용하여 더욱 쉽게 처리하기
* SpaCy 는 문서 구성요소를 다양한 구조에 나누어 저장하지 않고 요소를 색인화하여 검색 정보를 간단히 저장하는 라이브러리이다.

5. 불용어(Stop words) 처리
* 빈도 순으로 상위에 위치한 단어는 'the', 'and', 'i' 등의 단어가 있을 수 있고, 이런 단어는 분석하는데 그다지 도움이 되지 않는 단어이며 이를 불용어라 한다.
* NLP 라이브러리는 접속사, 관사, 부사, 대명사, 일반동사 등을 포함한 일반적인 불용어를 내장하고 있다.

6. 통계적 트리밍(Trimming)
* 불용어 처리와 같이 직접 단어를 추가하여 제거하지 않고도 통계 수치를 통해 말뭉치 내에서 너무 많거나, 적은 토큰을 제거(Trimming)하는 방법
* 등장 빈도가 너무 적은 단어는 분서 분류 차원에서 큰 의미를 갖지 못함
* 모든 단어를 불용어에 일일히 추가하기 어려우므로 통계적 트리밍 사용

7. 어간 추출(Stemming)과 표제어 추출(Lemmatization)
* 어간(stem)
  * 단어의 의미가 포함된 부분으로 접사등이 제거된 형태로 어근이나 단어의 원형과 같지 않을 수 있습니다. 예를 들어 argue, argued, arguing, argus의 어간은 단어들의 뒷 부분이 제거된 argu가 어간이다.
  * 알고리즘
    * Porter, Snowball, Dawson
* Lemmatization(표제어 추출)
  * 표제어 추출을 거친 단어들은 기본 사전형 단어 형태인 Lemma(표제어)로 변환됨
  * 명사의 복수형은 단수형으로, 동사는 모두 타동사로 변환
  * 단어의 표제어를 찾아가는 과정은 어간 추출에 비해 복잡하기 때문에 보다 많은 연산이 필요함

## 3. 등장 횟수 기반의 단어 표현 (Count-based Representation)
1. 텍스트 문서를 벡터로 표현
* 벡터화
  * 컴퓨터가 계산할 수 있도록 수치정보로 변환하는 과정
* 등장 횟수 기반의 단어 표현(Count-based Representation)은 단어가 특정 문서(혹은 문장)에 들어있는 횟수를 바탕으로 해당 문서를 벡터화
* 대표적인 방법
  * Bag-of-Words(TF, TF-IDF) 방식

2. Bag-of-Words(BoW) : TF(Term Frequency)
* 문서(혹은 문장)에서 문법이나 단어의 순서 등은 무시하고 단어들의 빈도만 고려하여 벡터화
* TF(Term Frequency)는 단순히 "문장에 해당하는 단어가 몇 번 등장하는지"를 사용하여 문서를 벡터화하는 방법
* 사이킷런(Scikit-learn, Sklearn) 의 CounterVectorizer 를 사용하면 TF 방식으로 문서를 벡터화 할 수 있음.

3. CountVectorizer 적용하기
* 순서
  * 단어를 토큰화
  * 말뭉치에 CountVectorizer를 적용
  * 적용한 결과를 문서-단어 행렬(Document-Term Matrix, DTM)으로 변환
  * CountVectorizer 로 제작한 문서-단어 행렬을 분석
```python
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
```

4. Bag-of-Words(BoW) : TF-IDF (Term Frequency - Inverse Document Frequency)
* 다른 문서에 잘 등장하지 않는 단어라면 해당 문서를 대표할 수 있는 단어가 될 수 있음
* 다른 문서에 적게 등장하는 단어에 가중치를 두는 방법이 TF-IDF(Term Frequency-Inverse Document Frequency)이다.
* TF-IDF의 수식
  * $\text{TF-IDF(w)} = \text{TF(w)} \times \text{IDF(w)}$
  * TF(Term Frequency)
    * $\text{TF(w)} = \text{특정 문서 내 단어 w의 수}$
  * IDF(Inverse Document Frequency)
    * 분류 대상이 되는 모든 문서의 수를 단어  w  가 들어있는 문서의 수로 나누어 준 뒤 로그를 취해준 값
    * $\text{IDF(w)} = \log \bigg(\frac{\text{분류 대상이 되는 모든 문서의 수}}{\text{단어 w가 들어있는 문서의 수}}\bigg)$
  * $\text{IDF(w)} = \log \bigg(\frac{n}{1 + df(w)}\bigg)$
    * $\text{분류 대상이 되는 모든 문서의 수} : n \\$
    * $\text{단어 w가 들어있는 문서의 수} : df(w)$

5. TfidfVectorizer 적용하기

6. 유사도를 이용해 문서를 검색
* 유사도 측정 방법
  * 코사인 유사도(Cosine Similarity)
    * 두 벡터가 이루는 각의 코사인 값을 이용하여 구할 수 있는 유사도
    * 수식
      * $\Large \text{cosine similarity} = cos (\theta)=\frac{A⋅B}{\Vert A\Vert \Vert B \Vert}$
    * 두 벡터의 방향이 완전히 같을 경우 1이며
    * 90도의 각을 이루면 0
    * 완전히 반대방향을 이루면 -1 이다.

* K-NearestNeighbor (K-NN, K-최근접 이웃)
  * 쿼리와 가장 가까운 상위 K개의 근접한 데이터를 찾아서 데이터의 유사성을 기반으로 점을 추정하거나 분류하는 방법

* N-gram
  * 자연어를 벡터로 표현할 때 2개 이상의 단어를 하나의 단위로 삼는 방법
  * 연속하는 2개 이상의 단어, 즉 단어 시퀀스(Word Sequence)를 벡터화
  * N에는 1,2,3... 과 같은 자연수 사용, N에 따라 단어 시퀀스를 몇 개의 단어로 구성할 지를 결정
  * N=1,2,3 인 경우를 각각 Uni-gram, Bi-gram, Tri-gram 이라 부르며 N이 4이상일 때에는 그냥 4-gram, 5-gram 의 방식으로 부른다.
  * N-gram의 문제점
    * 장기 의존성(Long-term dependency)
      * 해결방법: 
        * 의존성 분석(Dependency parsing)
          * Shift reduce parsing 과 같은 Transition-based Model과 토큰끼리의 의존성 구조를 그래프로 표현한 Graph-based Model이 있음.
        * N=1~5 까지 여러 N-gram을 섞어 사용하여 이런 문제를 해결
    * 희소성(Sparsity) 문제
      * N 을 증가시키면 이전에 살펴보았던 희소성 문제 발생
      * 해결방법:
        * 스무딩(Smoothing)과 백오프(Backoff) 라는 방법 사용
