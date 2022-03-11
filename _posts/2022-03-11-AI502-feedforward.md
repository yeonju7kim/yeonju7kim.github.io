---
layout: post
title: (AI502) 2.feedforward
date: 2022-03-11 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 AI502 수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## cost function

- negative log-likelihood
  - ![alt text](/public/img/220311/cost_function.png)
- MSE
  - ![alt text](/public/img/220311/cost_function2.png)
- cost function : maximum likelihood
  - $-logp(y|x)$
  - ![alt text](/public/img/220311/cost_function3.png)

## 여러가지 unit, activation 함수

- gaussian mixture?
- absolute value rectification
  - $g(z)=|z|$
- maxout
  - g(z)=max $z_j$
- softplus
  - $\sigma(z)=log(1+e^z)$
- hard-tanh, hard-softmax
  - ![alt text](/public/img/220311/hard-tanh-sigmoid.png)