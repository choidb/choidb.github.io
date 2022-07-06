---
title: '언어 모델과 RNN(Recurrent Neural Network, 순환 신경망)'
use_math: true
categories:
  - dl
---

**목차**  
[1. 언어 모델 (Language Model)](#1-언어-모델-language-model)  
[2. 순환 신경망 (RNN, Recurrent Neural Network)](#2-순환-신경망-rnn-recurrent-neural-network)  
[3. LSTM & GRU](#3-lstm--gru)  
[4. RNN 구조에 Attention 적용하기](#4-rnn-구조에-attention-적용하기)  



---
* Contents
1. 언어모델
2. 순환신경망(Recurrent Neural Network, RNN)
3. LSTM과 GRU
4. Attention

---

## 1. 언어 모델 (Language Model)
* 언어 모델(Language Model)이란 문장과 같은 단어 시퀀스에서 각 단어의 확률을 계산하는 모델
* 앞 단어 들이 등장했을 때 특정 단어가 등장할 확률을 **조건부 확률**로 구하게 된다


1. 통계적 언어 모델 (Statistical Language Model, SLM)
* 신경망 언어 모델이 주목받기 전부터 연구되어 온 전통적인 접근 방식입
* 통계적 언어 모델의 확률 계산
* 단어의 **등장 횟수**를 바탕으로 **조건부 확률**을 계산
* 통계적 언어 모델의 한계점
  * 횟수 기반으로 확률을 계산하기 때문에 희소성(Sparsity) 문제를 가짐
  * 실제로 사용되는 표현임에도 말뭉치에 등장하지 않았다는 이유로 많은 문장이 등장하지 못하게 되는 문제를 희소 문제라고 함
  * 개선:
    * N-gram 이나 스무딩(smoothing), 백오프(back-off)와 같은 방법이 고안됨

2. 신경망 언어 모델 (Neural Langauge Model)
* 횟수 기반 대신 Word2Vec이나 fastText 등의 출력값인 임베딩 벡터를 사용
* 말뭉치에 등장하지 않더라도 의미적, 문법적으로 유사한 단어라면 선택될 수 있음
  

## 2. 순환 신경망 (RNN, Recurrent Neural Network)
* RNN은 연속형 데이터를 처리하기 위해 고안된 신경망
  * 연속형 데이터 : 어떤 순서로 오느냐에 따라서 단위의 의미가 달라지는 데이터
* RNN 구조(세 가지 화살표가 존재함)
  * 입력 벡터가 은닉층에 들어가는 것을 나타내는 화살표
  * 은닉층로부터 출력 벡터가 생성되는 것을 나타내는 화살표
  * 은닉층에서 나와 다시 은닉층으로 입력되는 것을 나타내는 화살표(순환)
    * 출력 벡터가 다시 입력되는 특성 때문에 순환(Recurrent) 신경망 이라는 이름이 붙음
* 다양한 형태의 RNN
  * one-to-many : 1개의 벡터를 받아 Sequential한 벡터를 반환합니다. 이미지를 입력받아 이를 설명하는 문장을 만들어내는 이미지 캡셔닝(Image captioning)에 사용됩니다.
  * many-to-one : Sequential 벡터를 받아 1개의 벡터를 반환합니다. 문장이 긍정인지 부정인지를 판단하는 감성 분석(Sentiment analysis)에 사용됩니다.
  * many-to-many(1) : Sequential 벡터를 모두 입력받은 뒤 Sequential 벡터를 출력합니다. 시퀀스-투-시퀀스(Sequence-to-Sequence, Seq2Seq) 구조라고도 부릅니다. 번역할 문장을 입력받아 번역된 문장을 내놓는 기계 번역(Machine translation)에 사용됩니다.
  * many-to-many(2) : Sequential 벡터를 입력받는 즉시 Sequential 벡터를 출력합니다. 비디오를 프레임별로 분류(Video classification per frame)하는 곳에 사용됩니다.
* RNN의 장점과 단점
  * RNN의 장점
    * RNN은 모델이 간단하고 (이론적으로는) 어떤 길이의 sequential 데이터라도 처리할 수 있다는 장점을 가지고 있습니다.
  * RNN의 단점
    * RNN의 단점 1 : 병렬화(parallelization) 불가능
      * 벡터가 순차적으로 입력 된다
      * sequential 데이터 처리를 가능하게 해주는 요인이지만, 이러한 구조는 GPU 연산의 장점인 병렬화를 불가능하게 만든다.
      * 따라서, RNN 기반의 모델은 GPU 연산을 하였을 때 이점이 거의 없다
    * RNN의 단점 2: 기울기 폭발(Exploding Gradient), 기울기 소실(Vanishing Gradient)
      * 역전파 과정에서 문제 발생
      * 역전파 과정에서 RNN의 활성화 함수인 $\tanh$ 의 미분값을 전달하게 되는데 Recurrent가 반복된다고 볼 때, 반복해서 곱해주기 때문에 1보다 작으면 값이 점점 작아지게 되고 기울기가 소실된다. 만약 1보다 크다면 기울기 폭발(Exploding Gradient)이 일어난다.
      * 기울기 정보의 크기를 적절하게 조정하는 방법이 장단기 기억망(Long-Short Term Memory, LSTM)이다.

## 3. LSTM & GRU
* LSTM (Long Term Short Memory, 장단기기억망)
  * RNN에 기울기 정보 크기를 조절하기 위한 Gate를 추가한 모델
* 시퀀스 데이터를 다루기 위한 모델로 많이 사용
* LSTM의 구조
  * 기울기 소실 문제를 해결하기위해 3가지 게이트 추가함
    * Forget Gate ( ft ): 과거 정보를 얼마나 유지할 것인가?
    * Input Gate ( it ) : 새로 입력된 정보는 얼마만큼 활용할 것인가?
    * Output Gate ( ot ) : 두 정보를 계산하여 나온 출력 정보를 얼마만큼 넘겨줄 것인가?
  * hidden-state 말고도 활성화 함수를 직접 거치지 않는 상태인 cell-state 가 추가
    * cell-state는 역전파 과정에서 활성화 함수를 거치지 않아 정보 손실이 없기 때문에 뒷쪽 시퀀스의 정보에 비중을 결정할 수 있으면서 동시에 앞쪽 시퀀스의 정보를 완전히 잃지 않을 수 있습니다.

* GRU (Gated Recurrent Unit)
  * LSTM에서 있었던 cell-state가 사라졌습니다.
    * cell-state 벡터  ct  ​와 hidden-state 벡터  ht ​가 하나의 벡터  ht ​로 통일되었습니다.
  * 하나의 Gate  zt 가 forget, input gate를 모두 제어합니다.
    * zt 가 1이면 forget 게이트가 열리고, input 게이트가 닫히게 되는 것과 같은 효과를 나타냅니다.
    * 반대로  zt 가 0이면 input 게이트만 열리는 것과 같은 효과를 나타냅니다.
  * GRU 셀에서는 output 게이트가 없어졌습니다.
    * 대신에 전체 상태 벡터  ht  가 각 time-step에서 출력되며, 이전 상태의  ht−1  의 어느 부분이 출력될 지 새롭게 제어하는 Gate인  rt  가 추가되었습니다.

## 4. RNN 구조에 Attention 적용하기
* 기존 RNN 기반(LSTM, GRU) 번역 모델의 단점
  * RNN이 가진 가장 큰 단점 중 하나는 기울기 소실로부터 나타나는 장기 의존성(Long-term dependency) 문제
  *  Encoder의 정보를 Decoder로 넘겨줄 때, 입력되는 모든 단어 정보를 하나의 Hidden-state 벡터에만 담아야 한다
     *  &rArr; Attention(어텐션) 메커니즘으로 문제 해결
* Attention
  * Attention은 각 인코더의 Time-step 마다 생성되는 Hidden-state 벡터를 간직함
  * 모든 단어가 입력되면 생성된 Hidden-state 벡터를 모두 디코더에 넘겨줌
  * 디코더에서 Attention이 동작하는 방법
    * 디코더의 각 Time-step 마다의 Hidden-state 벡터는 쿼리(query)로 사용합니다.
    * 인코더에서 넘어온 N개의 Hidden-state 벡터를 키(key)와 밸류(value)로 사용합니다.
    * 쿼리와 키의 연관성은 내적(dot-product)을 사용하여 구합니다.
  * Attention 가중치가 구해지고 단어가 출력되는 과정
    * 쿼리(Query)로는 디코더의 Hidden-state 벡터, 키(Key)와 밸류(Value)로는 인코더에서 넘어온 Hidden-state 벡터를 준비합니다.
    * 쿼리와 키의 연관성을 구하기 위해서 각 벡터를 내적한 값을 구합니다.
    * 이 값에 소프트맥스(Softmax) 함수를 취해줍니다.
    * 소프트맥스의 결과값에 밸류(Value)인 인코더에서 넘어온 Hidden-state 벡터를 곱해줍니다.
    * 결과로 나오는 벡터를 모두 더해줍니다.
    * 이 벡터의 성분 중에는 쿼리-키 연관성이 높은 밸류 벡터의 성분이 더 많이 들어있게 됩니다.
    * 최종적으로 5에서 생성된 벡터와 디코더의 Hidden-state 벡터를 사용하여 출력 단어를 결정하게 됩니다.
      * 디코더는 단어를 생성할 때마다 위의 계산을 실시한다. 따라서 Time-step마다 출력할 단어가 어떤 인코더의 어떤 단어 정보와 연관되어 있는지, 즉 어떤 단어에 집중(Attention)할 지를 알 수 있다.
      * Attention을 활용하면 디코더가 인코더에 입력되는 단어 정보를 모두 활용하기 때문에 장기 의존성 문제를 해결할 수 있다.
