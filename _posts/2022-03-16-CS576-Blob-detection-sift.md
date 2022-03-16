---
layout: post
title: (CS576) Blob detection and SIFT
date: 2022-03-14 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 CS576 수업에서 제가 새로 배운 부분만 정리한 것입니다.

---

## edge detection

![alt image](/public/img/220316/edge_detection.png)

## blob detection

![alt image](/public/img/220316/laplacian_of_gaussian.png)

- laplacian은 gaussian과 등방향성이다.

![alt image](/public/img/220316/laplacian_gaussian.png)

- blob의 크기에 따라 response가 다르다. 그림과 달리 깊은 곳이 밝게 된다.

![alt image](/public/img/220316/response_map.png)

- blob의 반지름 R에 따라 최적의 $\sigma$가 다르다.
  - $\sigma = r/\sqrt{2}$

- $\sigma$가 커지면 response가 소멸된다.
  - 따라서 scale normalization을 한다.
  - $\nabla^2_{norm}g=\sigma^2\nabla^2g$

- Difference of Gaussians(DoG)
  - Laplacian은 두 다른 가우시안의 차이로 근사화할 수 있다.
  - ![alt image](/public/img/220316/Dog.png)

## SIFT

- blob 주위의 gradient를 계산하여 이를 이용해 histogram을 만들어서 유사도를 구하는 것
- 파노라마와 이미지 서치 등에 사용

> 1. blob detection으로 scale-space extrema를 찾는다.<br>
>   DoG를 이용하여 여러 조합으로 여러 크기의 blob을 찾는다.
> 2. keypoint filter<br>
>   DoG response가 특정 threshold보다 작으면 무시한다.
> 3. Orientation assignment<br>
>   ![alt image](/public/img/220316/orientation_assignment.png)<br>
>   dominant한 orientation을 찾은 후에 방향을 맞춘다.
> 4. Calculating descriptor<br>
>   8 quantized orientation으로 orientation 표현

- Sift의 장점
  - scale invariance
  - rotation invariance
  - insensitivity to other small variantion
  - insensitivity to illumination change(edge의 distribution을 보기 때문)
  - insensitivity to noise