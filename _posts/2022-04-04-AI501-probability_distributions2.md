---
layout: post
title: (AI501) 7. Commonly used probability distributions(2)
date: 2022-04-04 00:10:00 +0900
category: AI501
use_math: true
comments: true
---

본 포스팅은 AI501 수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## Beta distribution

- a와 b는 양수이다.
- 팩토리얼의 일반화
- ![alt image](/public/img/220405/beta.png)
- ![alt image](/public/img/220405/beta2.png)
- ![alt image](/public/img/220405/beta3.png)
- ![alt image](/public/img/220405/beta4.png)
  - b가 커지면 0에 치우쳐짐
  - a,b가 커지면 위로 높아짐
  - a,b가 작다면 아래로 낮아짐
  - a = 1, b = 1이면 1
- beta distribution은 bernoulli distribution의 conjugate prior이다. (conjugacy, 둘은 conjugate pair)
  - bernoulli likelihood + beta prior $\rightarrow$ beta posterior

## Binomial distribution

- ![alt image](/public/img/220405/binormial.png)
- bernoulli 분포를 따르는 m개의 data의 합은 binomial distribution을 따른다.
- Beta distribution은 binomial distribution의 conjugate prior (with
parameter π)

## Categorical distribution

- ![alt image](/public/img/220405/category.png)

## Multinomial distribution

- ![alt image](/public/img/220405/multinomial.png)

## Dirichlet distribution

- Categorical distribution, Multinomial distribution의 $\pi$의 prior distribution