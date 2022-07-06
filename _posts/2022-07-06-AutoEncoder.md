---
title: 'AutoEncoder'
use_math: true
categories:
  - dl
---

**목차**  
[1. AutoEncoder](#1-autoencoder)  
[2. Manifold Learning](#2-manifold-learning)  
[3. VAE](#3-vae)  




---
* Contents
1. AutoEncoder(AE)
2. Latent Vector(잠재 벡터)
3. 매니폴드(Manifold)
4. VAE(Variational AutoEncoder)


---

## 1. AutoEncoder
* 입력 데이터를 저차원의 벡터로 압축한 뒤 원래 크기의 데이터로 복원하는 신경망
<img src="https://github.com/choidb/choidb.github.io/blob/master/_posts/images3/2022-06-28-17-50-08.png?raw=true" width="400" height="200"/>

* Code 라고 표시된 가장 저차원의 벡터는 Latent(잠재) 벡터라고도 함
  * Latent(잠재) 벡터란 원본 데이터보다 차원이 작으면서도, 원본 데이터의 특징을 잘 보존하고 있는 벡터
* AutoEncoder의 대표적인 쓰임새
  * 차원 축소(Dimensionality Reduction)와 데이터 압축
  * 데이터 노이즈 제거(Denoising)
  * 이상치 탐지(Anomaly Detection)

## 2. Manifold Learning
[Manifold Learning 1](https://roytravel.tistory.com/105) 참고  
[Manifold Learning 2](https://deepinsight.tistory.com/124) 참고

## 3. VAE
[VAE(Variational AutoEncoder)](https://deepinsight.tistory.com/127) 참고
