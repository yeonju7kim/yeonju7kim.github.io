---
layout: post
title: vision transformer
date: 2022-02-25 00:10:00 +0900
category: transformer
use_math: true
comments: true
---
본 포스팅은 아래 논문을 참고했습니다.
<https://arxiv.org/pdf/2010.11929.pdf>

## 1. Introduction

자연어 처리에서 많이 쓰게 된 transformer를 이미지에도 적용해본 논문.

자연어 처리에서는 주로 큰 text corpus를 pre-train하고, 더 작은 task에 맞춰서 fine-tuning 했다. Transformer의 computational effciency와 scalability에서의 장점으로 아주 큰 데이터를 학습할 수 있게 됐다.

vision에서도 transformer를 사용하려는 노력이 많았다. 하지만 이론적으로는 효과적이었지만, specialized attention pattern의 사용으로 현대의 하드웨어 가속기에서는 효율적으로 scaled 되지 못했다. 

이 논문에서는 vision에도 transformer를 적용하기 위해 image를 patch로 나눴고, linear embedding을 했다. 그리고 patch를 transformer의 word처럼 적용했다.

중간 사이즈의 dataset인 imagenet으로 regularization을 적게 사용해서 학습을 시켰을 때는 성능이 좋지 않았다. 그 이유는 transformer는 부족한 데이터셋으로 학습할 때 inductive biases(예를 들어 equivariance와 locality)가 부족하기 때문이다.

하지만 큰 사이즈의 dataset을 사용할 때는 사이즈가 inductive bias를 이겼고, 좋은 성능을 냈다.

---

## 2. Related work

- 이미지에 self-attention을 pixel별로 적용하면, pixel 개수의 제곱의 cost가 들기 때문에 실제 이미지에 적용하기 어렵다. 이런 문제 때문에 인접한 부분만 self-attention 하는 방법도 사용됐는데, 이것은 convolution을 대체할 수 있었다. 

- 위에서 알 수 있듯 이미지에도 transformer를 적용할 수 있으려면 메모리 사용을 줄여야 한다. scalable approximation을 사용하는 sparse transformer, attention을 scale하는 방법등을 사용하기도 했다.(?)

- 2x2 patch를 추출해서 하는 방법도 있었다. 이것과 vit의 차이는 

---

## 3. Method

![alt text](/public/img/220)


#### 3.1 

