---
title: '합성곱 신경망(Convolutional Neural Network)과 전이 학습(Transfer Learning)'
use_math: true
categories:
  - dl
---

**목차**  
[1. CNN(Convolutional Neural Network, 합성곱 신경망)과 CNN의 구조](#1-cnnconvolutional-neural-network-합성곱-신경망과-cnn의-구조)  
[2. 전이학습 (Transfer Learning)](#2-전이학습-transfer-learning)  




---
* Contents
1. CNN(Convolutional Neural Network)
2. Convolution & Pooling Layer
3. 전이 학습(Transfer Learning)
4. 이미지 데이터 증강(Image Data Augmentation)

---

## 1. CNN(Convolutional Neural Network, 합성곱 신경망)과 CNN의 구조
* 합성곱 신경망은 학습 과정에서 공간적 특성을 보존하며 학습할 수 있다.
* 합성곱 층은 이미지의 일부분을 훑으면서 연산이 진행되며 특징을 잡아내어 학습하기 때문에
층이 깊어지더라도 공간적 특성을 최대한 보존할 수 있다.

* CNN의 구조
  * 합성곱 층(Convolution Layer)과 풀링 층(Pooling Layer)
  * 합성곱(Convolution)
    * 합성곱 필터(Convolution Filter)가 슬라이딩(Sliding)하며 이미지 부분부분의 특징을 읽어나간다.
    * Convolution에 적용할 수 있는 패딩(Padding)과 스트라이드(Stride)
      * 패딩(Padding)
        * 이미지 외부를 특정한 값으로 둘러싸서 처리해주는 방식
        * '0'으로 둘러싸주는 제로-패딩(Zero-Padding)이 가장 많이 사용
        * 연산되어 나오는 Output, 즉 Feature map 의 크기를 조절하고 실제 이미지 값을 충분히 활용하기 위해 사용
      * 스트라이드(Stride)
        * Stride 를 조절하면 슬라이딩(Sliding)시에 몇 칸 씩 건너뛸지를 나타냄
        * 필터 크기(Filter size), 패딩(Padding), 스트라이드(Stride)에 따른 Feature map 크기 변화
          * $N_{\text{out}} = \bigg[\frac{N_{\text{in}} + 2p - k}{s}\bigg] + 1$
            * $N_{\text{in}}$ : 입력되는 이미지의 크기(=피처 수) <br/>
            * $N_{\text{out}}$ : 출력되는 이미지의 크기(=피처 수) <br/>
            * $k$ : 합성곱에 사용되는 커널(=필터)의 크기 <br/>
            * $p$ : 합성곱에 적용한 패딩 값 <br/>
            * $s$ : 합성곱에 적용한 스트라이드 값
  * 풀링(Pooling)
    * 가로, 세로 방향의 공간을 줄이기 위함
    * 최대 풀링(Max pooling)과 평균 풀링(Average pooling) 존재
      * 최대 풀링(Max pooling)
        * 최대 풀링은 정해진 범위 내에서 가장 큰 값을 꺼내오는 방식이며 평균 풀링은 정해진 범위 내에 있는 모든 요소의 평균을 가져오는 방식
        * 일반적으로 이미지를 처리할 때에는 각 부분의 특징을 최대로 보존하기 위해서 최대 풀링을 사용
        * 풀링 층은 학습해야 할 가중치가 없으며 채널 수가 변하지 않는다
* 완전 연결 신경망(Fully Connected Layer) 구축하기

* CNN의 학습
  * CNN에서는 Convolution 층에 있는 Filter의 가중치가 학습이 된다.
  * 층이 깊어지면 Convolution 층과 Pooling 층을 거치면서 이미지가 작아지고 Convolution 층의 Filter는 더 큰 특징을 포착함

## 2. 전이학습 (Transfer Learning)
* 전이 학습은 대량의 데이터를 학습한 사전 학습 모델(Pre-trained Model)의 가중치를 그대로 가져온 뒤 분류기, 즉 완전 연결 신경망 부분만 추가로 설계하여 사용함
* 사전 학습 모델의 가중치는 대량의 데이터를 학습해서 얻어진다.
* 여러 데이터의 일반적인 특징을 많이 학습하였기 때문에 어떠한 데이터를 넣더라도 준수한 성능을 보임
* 일반적으로 사전 학습 가중치는 학습되지 않도록 고정(freeze)한 채로 진행되기 때문에
빠르게 좋은 결과를 얻을 수 있다

* 이미지 분류를 위한 주요 사전 학습 모델(Pre-trained Model)
  * VGG, Inception, ResNet
    * VGG
      * 모든 합성곱 층에서 3×3 크기의 필터 사용
        * 대신 층을 깊게 쌓음으로써 기존 7×7, 11×11 크기의 필터 이상의 표현력을 가질 수 있도록 함
      * 활성화 함수로 ReLU를 사용하고 가중치 초깃값으로는 He 초기화을 사용
        * 층을 깊게 쌓았음에도 기울기 소실(Gradient vanishing)문제기 빌셍하지 않음
      * 마지막으로 완전 연결 층에 드롭아웃(Dropout)을 사용하여 과적합 방지 및 옵티마이저는 아담(Adam) 사용
    * GoogLeNet(Inception)
      * 기본적인 합성곱 신경망이 결합된 형태
      * 세로 방향의 깊이 뿐만 아니라 가로 방향으로도 넓은 신경망 층을 가지고 있다
        * 가로 방향으로 층을 넓게 구성한 것을 인셉션(Inception) 구조라고 한다.
      * 인셉션 구조를 활용하여 크기가 다른 필터와 풀링을 병렬적으로 적용한 뒤 결과를 조합
    * ResNet  
    <img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images3/2022-06-28-17-20-57.png?raw=true" width="400" height="280"/>  
    
      * 화살표는 ResNet의 특징인 Residual Connection(=Skipped Connection)이다.
      * 층을 거친 데이터의 출력에 거치지 않은 출력을 더해준다.
      * 역전파 과정에서 미분을 적용하더라도 1 이상의 값으로 보존되기 때문에 층이 깊어짐에 따라 발생하는 기울기 소실(Vanishing Gradient) 문제를 어느정도 해결할 수 있다.
* 이미지 증강(Image Augmentation)
  * 회전, 반전, 자르기, 밝기 혹은 채도 변화 등을 통해 데이터를 늘리는 방법
  * 일반화(Generalization)가 잘 되는 모델을 만들기 위해서 학습 데이터셋에 있는 이미지를 일부러 회전하거나 기울여서 나타내는 방법들을 이미지 데이터 증강(Image Data Augmentation)이라 한다.
