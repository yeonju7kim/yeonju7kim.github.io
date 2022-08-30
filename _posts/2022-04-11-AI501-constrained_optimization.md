---
layout: post
title: (AI501) 9. Constrained optimization
date: 2022-04-11 00:10:00 +0900
category: AI501
use_math: true
comments: true
---

본 포스팅은 AI501 수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## constrained optimization

![alt image](/public/img/220411/constrained_optimization.png)

## Convex sets

- ![alt image](/public/img/220411/convex.png)
- ![alt image](/public/img/220411/convex_definition.png)
- local minimum = global optimum

- convex set
  - empty set, singleton set, entire spae $R^d$
  - norm ball
  - hyperplane
  - halfspace
  - Affine transform

- convex set 특징
  - ![alt image](/public/img/220411/convex_set_attribute.png)

- convex function
  - constant function
  - exponential
  - power function of absolute value
  - pointwise max function
  - log-sum-exp(soft-version of max) : 확률이 너무 작아서 log 취함
  - affine function
  - quadratic function

- convex function 특징
  - ![alt image](/public/img/220411/convex_function_attribute.png)

## Convex optimization problems

- ![alt image](/public/img/220411/convex_optimization_problem.png)
- f, g 가 convex하고, h가 affine일 때, Convex optimization problems이다.
- feasible set : 모든 constraints를 만족하는 optimization variable 집합

## Lagrangian and Lagrange multipliers

- primal problem
  - ![alt image](/public/img/220411/primal_problem.png)
- Lagrangian
  - ![alt image](/public/img/220411/Lagrangian.png)
  - Lagrangian multiplier : $\lambda, \nu$
- ![alt image](/public/img/220411/primal_problem_solution.png)
  - 조건을 안지키면 $\inf$가 됨
  - $\lambde$가 0일 때 제일 큼(supremum)
  - 