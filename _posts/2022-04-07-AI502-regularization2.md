---
layout: post
title: (AI502) 5. regularization2
date: 2022-04-07 00:10:00 +0900
category: AI502
use_math: true
comments: true
---

본 포스팅은 AI502수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## Bagging

- training data를 ramdom-sampling해서 model을 각각 학습시키고, averaging하거나 voting한다.
- smaller variance
  - ![alt image](/public/img/220411/bagging_variance.png)

## Dropout

- 대부분의 sub-network는 학습이 되지 않는다.
- fast approximation
- geometric mean
  - ![alt image](/public/img/220411/geometric_mean.png)
  - ![alt image](/public/img/220411/normalize_probability.png)
  - ![alt image](/public/img/220411/p_ensemble.png)
  - ![alt iamge](/public/img/220411/predictive_distribution.png)
- maxout activation과 같이쓰면, 각 유닛은 비슷하게 학습된다.
  - ![alt image](/public/img/220411/maxout_dropout.png)

> - 장점
>   - effective 성능
>   - computationally cheap
>   - dropout은 distributed representation을 쓰는 어떤 모델과도 잘 어울린다.

- co-adaptation 피함
  - 몇몇 뉴런이 다른 뉴런에 dependent 해지는 것

- sparse activations

- Drop connect
- Gaussian Dropout
  - dropout을 generalize하는 방법으로는 noise injection을 하는 방법이 있다.
  - ![alt image](/public/img/220411/dropout_noise.png)

## Early Stopping = L2-Regularization

- Early Stopping
  - ![alt image](/public/img/220411/cost_function.png)
  - ![alt image](/public/img/220411/cost_function_final.png)
- L2 Regularization
  - ![alt image](/public/img/220411/l2_regularization.png)
- $\epsilon, \alpha, \tau$를 잘 골라서 두 식을 갖게 만들 수 있다.

## Batch Normalization

- ![alt image](/public/img/220411/batch_norm.png)
- internal covariate shift problem 해소
- generalization 성능 향상, converge 더 빨리
- learning rate에 덜 sensitive함
- loss surface를 더 smoother
  - ![alt image](/public/img/220411/smooth_loss_surface.png)
  - perturbation에 덜 sensitive, more predictable gradient

## Weight Tying (Parameter Sharing)

- 같은 Conv filter 사용, RNN에서 같은 weight 사용하는 것

## Data Augmentation

- input이나 hidden unit에 noise 추가