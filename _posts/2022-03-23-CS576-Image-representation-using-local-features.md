---
layout: post
title: (CS576) Image representation using local features
date: 2022-03-23 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 CS576 수업에서 제가 새로 배운 부분만 정리한 것입니다.

---

## Image Classification pipeline

1. regions 추출
    - Blob detection
2. descriptors 계산
    - SIFT
3. clusters 하고 frequencies 계산 (여러 이미지 사이에)
    - k-mean clustering (최적의 솔루션 찾을 수 없음, 다른 초기값을 가지도록 여러 모델을 돌려서 최적의 모델을 찾음)
      - k cluster center를 설정
      - 모든 데이터를 가까운 class로 설정
      - 다시 center 정함
    - BoW
      - geometric information이 없다는 단점
    - Dense descriptors
      - dense image grid에서 sift 추출
    - spatial pyramid
      - different level로 region을 다양하게 나눠서 사용
    - dense keypoints를 얻은 후, tilting을 하여 robustness를 포기하고 information을 얻음.
4. compute distance matrix
    - Nonparameteric approach
      - nearest neighbor (outlier에 sensitive하다)
      - KNN : K closed examples
        - runtime complexity
        - outlier에 sensitivity함
        - high-dimensional space에서 similarity를 계산
    - Parameteric approach
      - linear model
5. classification(SVM)

