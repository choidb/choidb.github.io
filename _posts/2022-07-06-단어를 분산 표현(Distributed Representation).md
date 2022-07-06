# 단어를 분산 표현(Distributed Representation)으로 나타내기

**목차**  
[1. 분산 표현(Distributed Representation)](#1-분산-표현distributed-representation)  
[2. Word2Vec](#2-word2vec)  
[3. fastText](#3-fasttext)  



---
* Contents
1. 임베딩(Embedding)
2. Word2Vec(CBoW, Skip-gram)
3. GloVe



---

## 1. 분산 표현(Distributed Representation)
* 분포 가설에 기반하여 주변 단어 분포를 기준으로 단어의 벡터 표현이 결정

1. 원-핫 인코딩(One-hot Encoding)
* 범주형 변수(Categorical feature)를 벡터로 나타내는 방법
* 단어 간 유사도를 구할 수 없다.
  * 코사인 유사도(cosine similarity): 단어 간 유사도를 구할 때 사용
    * $\large \text{Cosine similarity} = \frac{\vec{a} \cdot \vec{b} }{\vert \vec{a} \vert \vert \vec{b} \vert }$
  * 원-핫 인코딩을 적용한 서로 다른 두 벡터의 내적은 항상 0이므로, 어떤 두 단어를 골라 코사인 유사도를 구하더라도 그 값은 0이 되므로 두 단어 사이의 관계를 전혀 알 수 없다

2. 임베딩(Embedding)
* 원-핫 인코딩의 단점을 해결
* 단어를 고정 길이의 벡터, 즉 차원이 일정한 벡터로 나타낸다
* 벡터 내의 각 요소가 연속적인 값을 가짐
* 대표적인 방법: Word2Vec

## 2. Word2Vec
* 단어를 벡터로(Word to Vector) 나타내는 방법
* 가장 널리 사용되는 임베딩 방법 
* Word2Vec 에는 CBoW와 Skip-gram의 2가지 방법이 있음
1. CBoW 와 Skip-gram
* CBoW와 Skip-gram의 차이
  * 주변 단어에 대한 정보를 기반으로 중심 단어의 정보를 예측하는 모델인지 ▶️ CBoW(Continuous Bag-of-Words)
  * 중심 단어의 정보를 기반으로 주변 단어의 정보를 예측하는 모델인지 ▶️ Skip-gram
* 역전파 관점에서 보면 Skip-gram에서 훨씬 더 많은 학습이 일어나기 때문에 Skip-gram의 성능이 조금 더 좋게 나타남
* 계산량이 많기 때문에 Skip-gram에 드는 리소스가 더 크다.

2. Word2Vec 모델의 구조
* 입력 : Word2Vec의 입력은 원-핫 인코딩된 단어 벡터입니다.
* 은닉층 : 임베딩 벡터의 차원수 만큼의 노드로 구성된 은닉층이 1개인 신경망입니다.
* 출력층 : 단어 개수 만큼의 노드로 이루어져 있으며 활성화 함수로 소프트맥스를 사용합니다.

3. Word2Vec 학습을 위한 학습 데이터 디자인
* 예) The tortoise jumped into the lake
* 중심 단어 : The, 주변 문맥 단어 : tortoise, jumped
  * 학습 샘플: (the, tortoise), (the, jumped)
* 중심 단어 : tortoise, 주변 문맥 단어 : the, jumped, into
  * 학습 샘플: (tortoise, the), (tortoise, jumped), (tortoise, into)
* 중심 단어 : jumped, 주변 문맥 단어 : the, tortoise, into, the
  * 학습 샘플: (jumped, the), (jumped, tortoise), (jumped, into), (jumped, the)
* 중심 단어 : into, 주변 문맥 단어 : tortoise, jumped, the, lake
  * 학습 샘플: (into, tortoise), (into, jumped), (into, the), (into, lake)

4. Word2Vec의 결과
* 10000개의 단어에 대해 300차원의 임베딩 벡터가 생성
* 임베딩 벡터의 차원을 조절하고 싶다면 은닉층의 노드 수를 줄이거나 늘릴 수 있다.

5. Word2Vec으로 임베딩한 벡터 시각화
* Word2Vec을 통해 얻은 임베딩 벡터는 단어 간의 의미적, 문법적 관계를 잘 나타냄

## 3. FastText
* fastText 는 Word2Vec 방식에 철자(Character) 기반의 임베딩 방식을 더해준 새로운 임베딩 방식
* fastText가 고안된 이유
1. OOV(Out of Vocabulary) 문제
* Word2Vec 은 말뭉치에 등장하지 않은 단어에 대해서는 임베딩 벡터를 만들지 못한다는 단점이 있음
* 적게 등장하는 단어(Rare words)에 대해서는 학습이 적게 일어나기 때문에 적절한 임베딩 벡터를 생성해내지 못한다는 것도 Word2Vec 의 단점
* 기존 말뭉치에 등장하지 않는 단어가 등장하는 문제를 OOV(Out of Vocabulary) 문제라고 한다.

1. 2) 철자 단위 임베딩(Character level Embedding)
* fastText가 Character-level(철자 단위) 임베딩을 적용하는 법 : Character n-gram
  * fastText 는 3-6개로 묶은 Character 정보(3-6 grams) 단위를 사용
  * 3-6개 단위로 묶기 이전에 모델이 접두사와 접미사를 인식할 수 있도록 해당 단어 앞뒤로 "<", ">" 를 붙여줍니다.
  * 그리고 나서 해당 단어를 3-6개 Character-level로 잘라서 임베딩을 적용
  * 

2. 3) 철자 단위 임베딩 시각화