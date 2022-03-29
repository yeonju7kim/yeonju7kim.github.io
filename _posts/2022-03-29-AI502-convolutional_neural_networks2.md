---
layout: post
title: (AI502) 3. CNN(2)
date: 2022-03-29 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 AI502수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

- DeConvNet : feature을 pixel로 바꾸는 것
- 요즘 트랜드 : smaller strides, smaller filters
  - larger filter size는 extremely high, low feature를 학습함.
  - large stride는 aliasing effect를 가진다.
- Semantic Segmentation은 DeconvNet을 이용한다.

- Code로 image를 복원
  - ![alt image](/public/img/220329/visualizeCNNcode.png)
  - Image prior regularization : 실제 이미지처럼 보이게함, less spikes
  - 하나의 code로 여러개의 image를 합성가능

- Global Average Pooling
  - ![alt image](/public/img/220329/globalAveragePooling.png)
  - fc layer와 달리 feature map을 평균내서 output을 내는 방법

- Orthogonal Regularization
  - vanishing나 exploding를 방지

- network in network
  - train faster
  - 적은 수의 parameter로 비교적 높은 accuracy, training time 줄임(reduce computation)

- Vanishing gradient
  - auxiliary output
  - residual network
  - DenseNet
    - ![alt image](/public/img/220329/densenet.png)
    - fewer parameter, redundant feature map을 다시 학습하지 않는다.
    - 모든 complexity level의 feature를 사용한다.