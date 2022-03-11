---
layout: post
title: (AI501) 2.linear algebra - analytic geometry
date: 2022-03-10 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 AI501 수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## Norm

![alt text](/public/img/220310/norm.png)

- l2 norm : 계산, 최적화 쉬움, dl에서 weight decay에 사용
- l1 norm : sparsity inducing norm, sparsifying 문제일때 사용, LASSO 알고리즘에서 사용
- $l_{\infty}$ : x1, ..., xn까지 중에 가장 긴 vector
- l0 norm : norm 아님, x의 non-zero element의 개수

## vector norm

![alt text](/public/img/220310/vector_norm.png)

![alt text](/public/img/220310/vector_norm2.png)

## matrix norm

![alt text](/public/img/220310/vector_norm2.png)

