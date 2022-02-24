---
layout: post
title: Transformer 고찰
date: 2022-02-25 00:00:00 +0900
category: dl_paper
use_math: true
comments: true
---
# Transformer 고찰

아직 transformer에 대한 이해가 부족하다. 하지만 transfomer를 공부하면서 생각했던 것을 메모해두었다.

## Transformer 에 대해 생각해보게 된 배경

회사에서 cnn 모델만 사용했는데, cnn을 사용할 때, convolution 연산의 지역적인 특성을 가지고 연산을 한다는 점 때문에 문제가 많았다. 같은 이미지에서 조금만 변화가 있어도 inference가 잘 되지 않았다는 것이 문제였다. 구체적으로는 배경의 영향으로 inference 결과가 달라지거나(spurious한 model) object의 위치가 달라져서 inference 결과가 달라지는 것(brittle한 model)등이 당시의 문제였는데, 이에 대한 대책을 찾지 못했다. 
 
당시에는 이를 해결하려고 다양한 시도를 했었다. 잘못된 inference를 하게 되는 가장 큰 원인은 먼저 imbalanced data라고 생각을 했다. balance가 맞지 않는 데이터를 처리하려고 Class-Balanced Loss를 사용하거나 불량데이터를 합성해서 만들었다. 하지만 그 역시도 한계가 있었다.

그래서 object 위치가 조금만 달라져도 잘못된 추론을 하는 문제를 해결하기 위해 Augmentation으로 이미지에 여러 변화를 주어 학습하기도 하고, 배경의 영향을 크게 받는 부분을 줄이기 위해 불필요한 부분을 masked하기도 했다.

이제와서 생각해보니 이런 것들은 cnn이 가질 수 있는 문제였다. convolution kernel을 사용하여 추론한다는 것은 영상의 local(high-frequency) 정보로 추론하게 되므로 local 정보에 조금의 변화를 주는 adversarial attack에 약하다. 

transformer는 중요한 정보에 가중치를 두어 연산을 해서 추론하는 방법이다. 위치 정보가 embedding 되어 학습되긴 하지만, cnn처럼 인접한 정보를 연속적으로 묶어 local 정보에 집중하는 방법이 아니라서 위에서 말한 cnn이 단점을 어느정도 해소한다고 생각했다. 

## Transformer의 장점 (작성중)

- transformer는 중요한 정보에 가중치를 두어 학습하게 되기 때문에 중요하지 않은 정보까지 학습하는 cnn보다 성능이 좋다.

- 논문에서 처럼 computational complexity가 낮고, parallel한 computation으로 train과 inference 속도가 빠르고, path length가 짧다.

## Transformer의 한계 (작성중)

- 학습이 잘 될까?

- 만약 

## Transformer에서 궁금한 점 (작성중)

1. attention할 부분을 따로 라벨링 하는 것이 아닌데 어떻게 학습이 되지? 학습은 잘 될까? 처음에 pre-trained model을 만들때 시간이 오래 걸렸을까?

2. data 품질이 좋지 않은 것은 언제나 문제이다. 당연하게도 biased dataset으로 학습을 하면 bias가 학습된다. 많은 biased data로 학습을 할 경우 bias를 학습하게 되면 중요하지 않은 정보에 집중하게 될텐데 이것을 해결할 방법은 없을까? 예를 들어 biased가 되지 않은 소수의 data에 가중치를 두어 학습을 한다면? biased가 되었다는 것을 알 방법은 없을까?

3. 어떤 상황에서 attention이 중요하지 않은 정보에 집중을 하게 될까? data 품질이 나쁜 상황 말고도 어떤 상황이 있을까? 혹등고래 분류처럼 진짜 구별하기 힘든 데이터일때는 어떨까?