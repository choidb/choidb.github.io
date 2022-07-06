# GAN(Generative Adversarial Networks)

**목차**  
[1. GAN(Generative Adversarial Networks)](#1-gangenerative-adversarial-networks)  
[2. CycleGAN](#2-cyclegan)  
[3. GAN 종류](#3-gan-종류)  


---
* Contents
1. GAN
2. CycleGAN

---

## 1. GAN(Generative Adversarial Networks)
* 실제와 유사한 데이터를 만들어내는 생성모델
* [GAN](https://www.samsungsds.com/kr/insights/generative-adversarial-network-ai-2.html) 참고
  

## 2. CycleGAN
* CycleGAN 의 장점
  * 서로 변환하고 싶은 두 스타일의 이미지를 따로 구하더라도 좋은 성능을 보인다
* CycleGAN 의 원리
  * CycleGAN은 비슷한 이미지에 대해 1:1 매칭을 시켜 이미지를 학습하는 것이 아니기 때문에 A→B 혹은 B→A, 즉 이미지를 변환하면서 Input 정보가 유실되어 원본 이미지의 특성을 잃어버리게 될 수 있다.
  * 원본 데이터로 돌아갈 수 있을 정도로만 변환을 진행하기 위해서 A→B→A, B→A→B 로 돌아가는 Cycle 구조를 가지게 되었고 이 때문에 CycleGAN 이라는 명칭이 붙음

## 3. GAN 종류
* SSGAN(Semi-Supervised GAN) : Class 분류와 동시에 Fake/Real 여부를 분류할 수 있도록 설계된 GAN
* ACGAN(Auxiliary Classifier GAN) : Noise 와 Class 를 제공하면 해당 클래스에 속하는 이미지가 생성될 수 있도록 설계된 GAN
* StackGAN : Text를 이용해서 이미지를 생성할 수 있도록 설계된 GAN
* DiscoGAN : Cycle GAN 과 유사하게 특정 도메인의 이미지를 다른 도메인에 적용할 수 있도록 설계된 GAN
* StyleGAN : 기존 Style Transfer 를 위한 GAN 모델보다 월등히 뛰어난 고화질의 이미지를 생성하도록 설계된 GAN