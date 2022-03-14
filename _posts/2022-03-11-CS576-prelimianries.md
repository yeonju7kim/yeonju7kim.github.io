---
layout: post
title: (CS576) Prelimianries
date: 2022-03-11 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 CS576 수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## Eigen Decomposition

- A가 square, symmetric matrix
- ![alt image](/public/img/220311/eigen_decomposition.png)
- optimization problem에 사용되는 예시
  - object function : $min\lVert Ax\rVert ^2=min\lVert \lambda x\rVert ^2$
  - PCA : $A^TA$의 가장 큰 eigen-value를 갖는 eigen-vector 찾기

## Probability Axioms

- Sample space($\Omega$) : 모든 가능한 output
- Event space(E) : $\Omega$의 멱집합

## Bayes' Theorem

$P(A\Vert B)=\frac{P(B\Vert A)P(A)}{P(B)}$

posterior = likelihood x prior

## multivariate gaussian distribution

![alt image](/public/img/220311/gaussian_distribution.png)