---
layout: post
title: (CS576) Support Vector Machine for classification
date: 2022-03-28 00:10:00 +0900
category: CS576
use_math: true
comments: true
---

본 포스팅은 CS576 수업에서 제가 새로 배운 부분만 정리한 것입니다.

---

## Support Vector Machine(SVM)

- Max-margin classifier
- ![alt image](/public/img/220329/svm.png)
- ![alt image](/public/img/220329/svm_margin.png)
- margin을 maximize해서 학습한다.
  - ![alt image](/public/img/220329/svm_function.png)
  - ![alt image](/public/img/220329/lagrangian.png)
    - convex optimizer의 regulation
    - 위 식으로 $\frac{\delta L_p}{\delta w} = 0$, $\frac{\delta L_p}{\delta b} = 0$를 만족하는 w와 b를 찾는다.
    - ![alt image](/public/img/220329/svm_optimized.png)
    - ![alt image](/public/img/220329/svm_objective.png)
    - 항상 global optimum을 얻을 수 있다.
  
## Non-separable SVM

- Soft margin
  - 마진 평면을 넘어가는 인스턴스를 허용
  - ![alt image](/public/img/220330/soft_margin.png)
    - ![alt image](/public/img/220330/soft_margin_equation.png)
    - 파라미터 C는 허용되는 오류 양을 조절한다. C 값이 클수록 오류를 덜 허용하며 이를 하드 마진(hard margin)이라 부른다. 반대로 C 값이 작을수록 오류를 더 많이 허용해서 소프트 마진(soft margin)을 만든다.
- Kernel Method
  - ![alt image](/public/img/220330/kernel_svm.png)

## Multi-class SVM

- One-versus-all : one vs the others
- One-versus-one : true vs false