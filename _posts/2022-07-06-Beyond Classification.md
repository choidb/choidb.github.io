# Beyond Classification

**목차**  
[1. 분할(Segmentation)](#1-분할segmentation)  
[2. 객체 탐지/인식(Object Detection/Recognition)](#2-객체-탐지인식object-detectionrecognition)  




---
* Contents
1. Segmentation의 동작 방식 및 Semantic Segmentation/Instance Segmentation
2. Transpose Convolution
3. U-net 모델
4. Object Detection

---

## 1. 분할(Segmentation)
* 하나의 이미지에서 같은 의미를 가지고 있는 부분을 구분해내는 Task
* 의료 이미지, 자율주행, 위성 및 항공 사진 등의 분야에서 많이 사용
* 동일한 의미(사람, 자동차, 도로, 인도, 자연물 등)마다 해당되는 픽셀이 모두 레이블링 되어있는 데이터셋을 픽셀 단위에서 레이블을 예측한다.

* Semantic Segmentation vs (Semantic) Instance Segmentation
  * 의미적 분할(Semantic Segmentation)
    * 사람, 자동차 등 같은 개체에 대해서 모두 동일하게 라벨링하는 방식
  *  Instance Segmentation
     * 여러 명의 사람이 있을 경우 각각 다른 레이블로 분류하는 방식
* 대표적인 Segmentation Model: FCN(Fully Convolutional Networks), U-net
  * FCN(Fully Convolutional Networks)
    * 이미지 분류를 위한 신경망에 사용되었던 CNN의 분류기 부분, 즉 완전 연결 신경망(Fully Connected Layer) 부분을 합성곱 층(Convolutional Layer)으로 대체한 모델
    * Segmentation 은 픽셀별로 분류를 진행하기 때문에 원래 이미지와 비슷하게 크기를 키워주는 Upsampling을 해야 한다.
      * Upsampling
        * Convolution 과 Pooling 을 사용하여 이미지의 특징을 추출하는 과정을 Downsampling(디운샘플링)이라 하며, 반대로 원래 이미지의 크기로 키우는 과정을 Upsampling(업샘플링)이라 함
        * Upsampling 에는 기존 Convolution 과는 다른 Transpose Convolution 이 적용됨
        * Transpose Convolution 에서는 각 픽셀에 커널을 곱한 값에 Stride를 주어 나타냄으로써 이미지 크기를 키워나감
  * U-net
    * Downsampling 에서는 Convolution 과 Maxpooling 을 거치면서 이미지의 특징을 추출
    * Upsampling 에서는 Convolution 과 Transpose Convolution 을 거치면서 원본 이미지와 비슷한 크기로 복원
    * Upsampling 에서 Downsampling 출력으로 나왔던 Feature map 을 적당한 크기로 잘라서 붙여준 뒤 추가 데이터로 사용

## 2. 객체 탐지/인식(Object Detection/Recognition)
* 전체 이미지에서 레이블에 맞는 객체를 찾아내는 Task 
* 객체의 경계에 Bounding Box 라고 하는 사각형 박스를 만든 후, 박스 내의 객체가 속하는 클래스가 무엇인지를 분류함.
* IoU(Intersection over Union)
  * 객체 탐지를 평가하는 지표
  * Bounding Box 를 Ground-truth라고 한다.  
<img src="2022-06-28-17-42-07.png" width="250" height="200"/>  
<img src="2022-06-28-17-43-54.png" width="300" height="150"/>  
&rArr; Ground-truth/Prediction에 해당하는 Bounding Box 에 따라 IoU가 구해지는 예시

* 대표적인 객체 탐지 Model
  * Two Stage Detector
    * 일련의 알고리즘을 통해 객체가 있을 만한 곳을 추천받은(Region Proposal) 뒤에 추천받은 Region, 즉 RoI(Region of Interest)에 대해 분류를 수행하는 방식
    * R-CNN계열(R-CNN, Fast R-CNN, Faster R-CNN 등)
  * One Stage Detector
    * 특정 지역을 추천받지 않고 입력 이미지를 Grid 등의 같은 작은 공간으로 나눈 뒤 해당 공간을 탐색하며 분류를 수행하는 방식
    * 1-stage 모델로는 SSD(Single Shot multibox Detector)계열과 YOLO(You Only Look Once)계열