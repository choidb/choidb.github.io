---
title: 'Transformer'
use_math: true
categories:
  - dl
---

**목차**  
[1. Transformer](#1-transformer)  
[2. GPT & BERT](#2-gpt-bert)  

---
* Contents
1. Transformer
2. Positional Encoding
3. 사전 학습된 언어 모델(Pre-trained LM) - Pre-training과 Fine-tuning
4. GPT, BERT
5. BERT - MLM(Masked Language Model) 과 NSP(Next Sentence Prediction)

---

## 1. Transformer
* 자연어처리 모델 SOTA(State-of-the-Art)의 기본 아이디어는 거의 모두 트랜스포머를 기반으로 한다.
* 트랜스포머가 자연어처리가 아닌 다른 문제도 잘 풀고있기 때문에 컴퓨터 비전 쪽에서도 적용하려는 시도가 있으며, 멀티모달(Multi-Modal) 분야에도 적용되고 있다.
* RNN 기반 모델이 가진 구조적 단점은 단어가 순차적으로 들어온다
  * 시퀀스가 길수록 연산 시간이 길어짐 &rArr; Transformer가 해결
* Transformer
  * 모든 토큰을 동시에 입력받아 병렬 처리하기 때문에 GPU 연산에 최적화되어 있음
  * 트랜스포머는 인코더 블록과 디코더 블록이 6개씩 모여있는 구조이다.
  * 인코더 블록은 크게 2개의 sub-layer ▶️ [Multi-Head (Self) Attention, Feed Forward] 로 나눌 수 있다.
  * 디코더 블록은 3개의 sub-layer ▶️ [Masked Multi-Head (Self) Attention, Multi-Head (Encoder-Decoder) Attention, Feed Forward] 로 나눌 수 있다.
  * 트랜스포머에서는 병렬화를 위해 모든 단어 벡터를 동시에 입력받는다.
    * 어떤 단어가 어디에 위치하는지 알 수 없게 된다.
    * 컴퓨터가 단어의 위치를 알 수 있도록 위치 정보를 담은 벡터를 따로 제공해주어야 하고,
    * 단어의 상대적인 위치 정보를 담은 벡터를 만드는 과정을 Positional Encoding 이라 한다.
  * Positional Encoding  
$\begin{aligned}
\text{PE}_{\text{pos},2i} &= \sin \bigg(\frac{\text{pos}}{10000^{2i/d_{\text{model}}}}\bigg) \\
\text{PE}_{\text{pos},2i+1} &= \cos \bigg(\frac{\text{pos}}{10000^{2i/d_{\text{model}}}}\bigg)
\end{aligned}
$

* Transformer의 주요 메커니즘: Self-Attention (셀프-어텐션)
  * 번역하려는 문장 내부 요소의 관계를 잘 파악하기 위해서, 문장 자신에 대해 어텐션 메커니즘을 적용
  * 각각의 벡터의 역할
    * 쿼리(q)는 분석하고자 하는 단어에 대한 가중치 벡터입니다.
    * 키(k)는 각 단어가 쿼리에 해당하는 단어와 얼마나 연관있는 지를 비교하기 위한 가중치 벡터입니다.
    * 밸류(v)는 각 단어의 의미를 살려주기 위한 가중치 벡터입니다.
  * Self-Attention은 세 가지 가중치 벡터를 대상으로 어텐션을 적용한다.
    * 먼저, 특정 단어의 쿼리(q) 벡터와 모든 단어의 키(k) 벡터를 내적합니다. 내적을 통해 나오는 값이 Attention 스코어(Score)가 됩니다.
    * 트랜스포머에서는 이 가중치를 q,k,v 벡터 차원  dk  의 제곱근인  dk−−√  로 나누어줍니다.
      * 계산값을 안정적으로 만들어주기 위한 계산 보정으로 생각해주시면 됩니다.
    * 다음으로 Softmax를 취해줍니다.
      * 이를 통해 쿼리에 해당하는 단어와 문장 내 다른 단어가 가지는 관계의 비율을 구할 수 있습니다.
    * 마지막으로 밸류(v) 각 단어의 벡터를 곱해준 후 모두 더하면 Self-Attention 과정이 마무리됩니다.
* [Attention, Transformer(Self-Attention)](https://velog.io/@idj7183/Attention-TransformerSelf-Attention) 참고

* Multi-Head Attention
  * 여러 개의 Attention 메커니즘을 동시에 병렬적으로 실행
  * 각 Head 마다 다른 Attention 결과를 내어주기 때문에 앙상블과 유사한 효과를 얻을 수 있으며, 병렬화 효과를 극대화 할 수 있다.
* Layer Normalization & Skip Connection
  * 트랜스포머의 모든 sub-layer에서 출력된 벡터는 Layer normalization과 Skip connection을 거치게 된다.
  * Layer normalization의 효과는 Batch normalization과 유사함
    * 학습이 훨씬 빠르고 잘 되도록 한다.
  * Skip connection(혹은 Residual connection)은 역전파 과정에서 정보가 소실되지 않도록 합니다.
* Feed Forward Neural Network
  * 다음으로 FFNN(Feed forward neural network) 로 들어간다.
  * 은닉층의 차원이 늘어났다가 다시 원래 차원으로 줄어드는 단순한 2층 신경망
  * 활성화 함수(Activation function)으로 ReLU를 사용
  * $\text{FFNN}(x) = \max(0, W_1x + b_1) W_2 +b_2$
* Masked Self-Attention
  * Masked Self-Attention은 디코더 블록에서 사용하기 위해서 마스킹 과정이 포함된 Self-Attention
  * 트랜스포머에서는 타깃 문장 역시 한 번에 입력되기 때문에 해당 위치 타깃 단어 뒤에 위치한 단어는 Self-Attention에 영향을 주지 않도록 마스킹(Masking)을 해준다.
  * Self-Attention (without Masking) vs Masked Self-Attention
    * Self-Attention 메커니즘은 쿼리 행렬(Q)와 키 행렬(K)의 내적합니다. 결과로 나온 행렬을 차원의 제곱근 $\sqrt{d_k}$ 로 나누어 준 다음, Softmax를 취해주고 밸류 행렬(V)과 내적한다.
    * **Masked Self-Attention** 에서는 Softmax를 취해주기 전, 가려주고자 하는 요소에만 $-\infty$ 에 해당하는 매우 작은 수를 더해준다. 이 과정을 **마스킹(Masking)**이라고 한다. 마스킹된 값은 Softmax를 취해 주었을 때 0이 나오므로 Value 계산에 반영되지 않는다.
* Encoder-Decoder Attention
  * 디코더에서 Masked Self-Attention 층을 지난 벡터는 Encoder-Decoder Attention 층으로 들어감
  * 번역할 문장과 번역되는 문장의 정보 관계를 엮어주는 부분이다.
  * 구조
    * 디코더 블록의 Masked Self-Attention으로부터 출력된 벡터를 쿼리(Q) 벡터로 사용합니다.
    * 키(K)와 밸류(V) 벡터는 최상위(=6번째) 인코더 블록에서 사용했던 값을 그대로 가져와서 사용합니다.
    * Encoder-Decoder Attention 층의 계산 과정은 Self-Attention 했던 것과 동일합니다.
* Linear & Softmax Layer
  * 디코더의 최상층을 통과한 벡터들은 Linear 층을 지난 후 Softmax를 통해 예측할 단어의 확률을 구한다.

## 2. GPT, BERT
* GPT와 BERT는 트랜스포머 구조를 변형하여 만들어진 언어 모델
* 두 모델은 사전 학습된 언어 모델(Pre-trained Language Model) 이라는 공통점을 가진다.
* 사전학습에 필요한 데이터를 추가 학습시켜 모델의 성능을 최적화하는 방법이 전이 학습(Transfer Learning)이라 한다.

1. GPT
* Generative Pre-trained Transformer 의 약자
* 사전 학습 언어 모델은 크게 2가지 과정을 거친다.
  * 사전 학습(Pre-training)
    * 레이블링 되지 않은 대량의 말뭉치 $U = (u_1, \cdots , u_n)$ 에 대해 로그 우도 $L_1$ 을 최대화하는 방향으로 학습된다.
    * $L_1(U) = \sum_i \log P(u_i \vert u_{i-k}, \cdots, u_{i-1}; \Theta)$
  * Fine-tuning
    * 레이블링 된 말뭉치 $C = (x_1, \cdots , x_m)$ 에 대하여 로그 우도 $L_2$ 를 최대화하는 방향으로 학습된다.
      * $L_2(C) = \sum_{(x,y)} \log P(y \vert x_1, \cdots , x_m)$
    * 사전 학습이 끝난 모델에 우리가 하고자하는 태스크에 특화된(Task specific) 데이터를 학습
    * GPT의 경우 Fine-tuning에서 학습하는 데이터셋이 클 때는 보조 목적함수로 $L_1$ 을 추가하여 $L_3$로 학습하면 학습이 더 잘 진행됩니다.  
      * $L_3(C) = L_2(C) + \lambda \cdot L_1(C)$
* 모델 구조
  * 트랜스포머의 디코더(Decoder) 블록을 쌓아서 모델을 구성
  * GPT에서는 12개의 디코더 블록을 사용
  * GPT에서는 인코더를 사용하지 않기 때문에 디코더 블록내에 2개의 Sub-layer만 있음
  * 인코더를 사용하지 않기 때문에 Encoder-Decoder Attention 층이 빠진다.
    * (트랜스포머의 디코더 블록에는 Masked Self-Attention, Encoder-Decoder Attention, Feed-Forward 층이 있음)

2. BERT
* BERT(Bidirectional Encoder Representation by Transformer)
* BERT는 트랜스포머의 인코더 블록을 12개 쌓아올린 모델
* BERT 구조
  1. Special Token : [CLS], [SEP]
      * [CLS] : Classification
        * [CLS] 토큰은 입력의 맨 앞에 위치하는 토큰
        * NSP(Next Sentence Prediction)이라는 학습을 위해 존재
      * [SEP] : Separation
        * BERT는 사전 학습 시에 텍스트를 2부분으로 나누어 넣으며, [SEP] 토큰은 첫 번째 부분의 끝자리와 두 번째 부분의 끝자리에 위치
  2. Input Vector : Token Embeddings, Segment Embeddings, Position Embeddings
      * Token Embeddings : 단어를 나타내는 임베딩입니다. Word2Vec, GloVe, FastText 등으로 사전 학습된 임베딩 벡터를 사용합니다.
      * Segment Embeddings : 첫 번째 부분과 두 번째 부분을 구분하기 위한 임베딩입니다.
        * [CLS] 부터 첫 번째 [SEP] 까지 동일한 벡터를 적용하고, 다음 토큰부터 두 번째 [SEP] 까지 동일한 벡터를 적용합니다.
      * Positional Embeddings : 단어의 위치를 나타내기 위한 임베딩입니다.
* BERT의 사전 학습(Pre-training) 방법들
  * Pre-trained Language Model이기 때문에 사전 학습 이후에 Fine-tuning을 진행
  * BERT의 사전 학습에서 사용되는 2가지 방법(MLM, NSP)
    * MLM(Masked Language Model)
      * 사전 학습 과정에서 레이블링 되지 않은 말뭉치 중에서 랜덤으로 15%가량의 단어를 마스킹하고 마스킹된 위치에 원래 있던 단어를 예측하는 방식으로 학습을 진행한다. (빈칸채우기와 비슷)
    * NSP(Next Sentence Prediction)
      * 모델이 문맥에 맞는 이야기를 하는지 아니면 동문서답을 하는지를 판단하며 학습하는 방식

